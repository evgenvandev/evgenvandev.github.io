---
layout: default
title: DVDManagement
parent: Java and SQLite
grand_parent: Java
nav_order: 2
has_toc: false
---

# DVDManagement
{: .no_toc }

## Оглавление
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## Описание

[Ссылка на источник на _GitHub_](https://github.com/eliaskone/Java-SQLite-GUI)

A Java application, which connects to a sqlite database, with which it is possible to insert, delete, 
or change entries in the database. The data inside the database is visualy shown in the application.

Приложение Java, которое подключается к базе данных sqlite, с помощью которой можно вставлять, удалять 
или изменять записи в базе данных. Данные внутри базы данных визуально отображаются в приложении.

![DVDApplication-1]({{ site.url }}{{ site.baseurl }}/assets/images/java/java-sqlite/DVDApplication.png "DVDApplication-1")

---

## Класс GUI (файл _GUI.java_) с методом main

{% capture code_fence %}
```java
//https://github.com/eliaskone/Java-SQLite-GUI
package sample.net.sqlitetutorial;

import javafx.application.Application;
import javafx.event.EventHandler;
import javafx.scene.Scene;
import javafx.scene.control.*;
import javafx.scene.control.cell.PropertyValueFactory;
import javafx.scene.control.cell.TextFieldTableCell;
import javafx.scene.image.Image;
import javafx.scene.layout.HBox;
import javafx.scene.layout.VBox;
import javafx.stage.Stage;

import java.sql.Connection;
import java.sql.ResultSet;
import java.util.ArrayList;

public class GUI extends Application {
    TableView<DVDReturn> tableView = new TableView<>();
    int int1, int2;
    String str1, str2;

    @Override
    public void start(Stage primaryStage) {
        TableFunctions tableFunctions = new TableFunctions();
        Connection connection = tableFunctions.connect();
        TableFunctions.createNewTable();

        tableView.setEditable(true);

        TableColumn id_colum = new TableColumn("id");
        TableColumn titel_colum = new TableColumn("titel");
        TableColumn director_colum = new TableColumn("director");
        TableColumn year_colum = new TableColumn("year");

        Stage stage = primaryStage;
        HBox hBox = new HBox();

        Button buttonAdd = new Button("New entry");
        Button buttonDel = new Button("Delete entry");
        buttonAdd.setMinSize(100,50);
        buttonDel.setMinSize(100,50);
        VBox vBox = new VBox(buttonAdd, buttonDel);

        ResultSet DataresultSet = tableFunctions.getData(connection);

        tableView.getColumns().addAll(id_colum, titel_colum, director_colum, year_colum);
        ArrayList <DVDReturn> dvdData = tableFunctions.createDVDList(DataresultSet);
        tableView.getItems().addAll(dvdData);

        id_colum.setCellValueFactory(new PropertyValueFactory<DVDReturn, Integer>("id"));
        titel_colum.setCellValueFactory(new PropertyValueFactory<DVDReturn, String>("titel"));
        director_colum.setCellValueFactory(new PropertyValueFactory<DVDReturn, String>("director"));
        year_colum.setCellValueFactory(new PropertyValueFactory<DVDReturn, Integer>("year"));

        buttonAdd.setOnAction(e->{
            Button btnConfirm = new Button("Confirm");

            TextField txtid = new TextField();
            TextField txtTitel = new TextField();
            TextField txtDirector = new TextField();
            TextField txtYear = new TextField();

            Label lblId = new Label("ID");
            Label lblTitel = new Label("Titel");
            Label lblDirector = new Label("Director");
            Label lblYear = new Label("Year");
            Label lblSpace = new Label("");

            Dialog dialog = new Dialog();
            DialogPane dialogPane = new DialogPane();
            dialog.setDialogPane(dialogPane);
            dialogPane.setContent(new VBox(4, new HBox(lblId, txtid), new HBox(lblTitel, txtTitel),
                    new HBox(lblDirector, txtDirector), new HBox(lblYear, txtYear), new HBox(lblSpace),
                    new HBox(lblSpace), new HBox(btnConfirm)));
           dialogPane.getButtonTypes().add(new ButtonType("Cancel", ButtonBar.ButtonData.CANCEL_CLOSE));
           dialog.show();

           btnConfirm.setOnAction(event -> {
               try {
                   int1 = Integer.valueOf(txtid.getText());
                   str1 = txtTitel.getText();
                   str2 = txtDirector.getText();
                   int2 = Integer.valueOf(txtYear.getText());

                   DVDReturn dvdReturn = new DVDReturn(int1, str1, str2, int2);
                   TableFunctions.dvdArray.add(dvdReturn);
                   TableFunctions.updateRow(int1, str1, str2, int2);
                   tableView.getItems().add(dvdReturn);
               }
               catch (NumberFormatException String){
                   Label lv = new Label("Try Again!");
                   Dialog dlgNotWorking = new Dialog();
                   DialogPane dp = new DialogPane();
                   dlgNotWorking.setDialogPane(dp);
                   dp.setContent(new VBox(4, new HBox(lv)));
                   dp.getButtonTypes().add(new ButtonType("Cancel", ButtonBar.ButtonData.CANCEL_CLOSE));
                   dlgNotWorking.show();
               }
           });
        });

        buttonDel.setOnAction(event -> {
            Label label = new Label("Do you really want to delete that Entry?");
            Dialog dialog = new Dialog();
            DialogPane dialogPane = new DialogPane();
            dialog.setDialogPane(dialogPane);
            Button btncnfm = new Button("Confirm");
            dialogPane.setContent(new VBox(4, new HBox(label), new HBox(btncnfm)));
            dialogPane.getButtonTypes().add(new ButtonType("Cancel", ButtonBar.ButtonData.CANCEL_CLOSE));

            dialog.show();

            btncnfm.setOnAction(event1 -> {
                TableFunctions.delete(tableView.getSelectionModel().getSelectedItem().getId());
                DVDReturn slctedentry = tableView.getSelectionModel().getSelectedItem();
                tableView.getItems().remove(slctedentry);
            });

        });

        titel_colum.setCellFactory(TextFieldTableCell.forTableColumn());
        titel_colum.setOnEditCommit(new EventHandler<TableColumn.CellEditEvent>() {
            @Override
            public void handle(TableColumn.CellEditEvent event) {
                EditValues(event, "titel");
            }
        });
        director_colum.setCellFactory(TextFieldTableCell.forTableColumn());
        director_colum.setOnEditCommit(new EventHandler<TableColumn.CellEditEvent>() {
            @Override
            public void handle(TableColumn.CellEditEvent event) {
                EditValues(event, "director");
            }
        });
        hBox.getChildren().addAll(tableView, vBox);

        Scene scene = new Scene(hBox);
        Image Icon = new Image(getClass().getResourceAsStream("database3.png"));
        stage.setScene(scene);
        stage.setTitle("DVD-Management");
        stage.getIcons().add(Icon);
        stage.show();
    }

    public void EditValues(TableColumn.CellEditEvent<DVDReturn, String> dvdStringCellEditEvent, String type){
        try {
            DVDReturn dvd = tableView.getSelectionModel().getSelectedItem();
            String newVal = dvdStringCellEditEvent.getNewValue();
            if(type == "titel") {
                TableFunctions.update("titel", newVal, dvd.getId());
                dvd.setTitel(newVal);}
            else if(type == "director"){
                TableFunctions.update("director", newVal, dvd.getId());
                dvd.setDirector(newVal);}
        }catch (Exception e){
            e.printStackTrace();
        }

    }

    public static void main(String[] args) {
        launch(args);
    }
}
```
{% endcapture %}
{% assign code_fence = code_fence | markdownify %}
{% include fix_linenos.html code=code_fence %}

---

## Класс TableFunctions (файл _TableFunctions.java_)

{% capture code_fence %}
```java
package sample.net.sqlitetutorial;

import java.nio.file.Path;
import java.nio.file.Paths;
import java.sql.*;
import java.util.ArrayList;

public class TableFunctions {
    static Path currentRelativePath = Paths.get("");
    static String s = currentRelativePath.toAbsolutePath().toString();
    static ArrayList<DVDReturn>dvdArray = new ArrayList<>();
    static ResultSet resultSet = null;
	
    public static Connection connect() {
        // SQLite connection string
        //String url = "jdbc:sqlite:"+s+"\\src\\sample\\net\\sqlitetutorial\\dvd.db";
        String url = "jdbc:sqlite:"+s+"\\sample\\net\\sqlitetutorial\\dvd.db";
        Connection connection = null;
        try {
			Class.forName("org.sqlite.JDBC");
            connection = DriverManager.getConnection(url);
        } catch (ClassNotFoundException | SQLException e) {
            System.out.println(e.getMessage());
        }
        return connection;
    }

    public static void delete(int id) {
        String sql = "DELETE FROM DVD WHERE id = ?";

        try (Connection connect = connect();
             PreparedStatement del = connect.prepareStatement(sql)) {
            del.setInt(1, id);
            del.executeUpdate();

        } catch (SQLException e) {
            System.out.println(e.getMessage());
        }
    }

    public static void updateRow(int id, String titel, String director, int year){
        String sql = "INSERT INTO DVD VALUES('"+id+"', '"+titel+"', '"+director+"', '"+year+"')";

        try (Connection connect = connect();
             PreparedStatement updateRow = connect.prepareStatement(sql)){
            updateRow.executeUpdate();

        }catch (SQLException e) {
            System.out.println(e.getMessage());
        }
    }

    public static void update(String index, String content, int id) {
        String sql = "UPDATE dvd SET "+index+"='"+content+"' WHERE id='"+id+"';";
        try (Connection connect = connect();
             PreparedStatement update = connect.prepareStatement(sql)) {
            update.executeUpdate();
        } catch (SQLException e) {
            System.out.println(e.getMessage());
        }
    }

    public static void createNewTable() {
        //String url = "jdbc:sqlite:"+s+"\\src\\sample\\net\\sqlitetutorial\\dvd.db";
        String url = "jdbc:sqlite:"+s+"\\sample\\net\\sqlitetutorial\\dvd.db";

        String sql = "CREATE TABLE IF NOT EXISTS DVD (\n"
                + "	id integer PRIMARY KEY,\n"
                + "	titel text NOT NULL,\n"
                + "	director text NOT NULL,\n"
                + "	year integer NOT NULL\n"
                + ");";
        try (Connection connection = DriverManager.getConnection(url);
             Statement statement = connection.createStatement()) {
            // create a new table
            statement.execute(sql);
        } catch (SQLException e) {
            System.out.println(e.getMessage());
        }
    }
    public static ResultSet getData(Connection connection){
        String sql = "Select * from DVD";
        try {
            PreparedStatement gettingData = connection.prepareStatement(sql);
            resultSet = gettingData.executeQuery();
            System.out.println(resultSet);
        }catch (SQLException e){
            e.printStackTrace();
        }
        return resultSet;
    }

    public static ArrayList<DVDReturn> createDVDList(ResultSet resultSet){
            try {
                while (resultSet.next()){
                    dvdArray.add(new DVDReturn(resultSet.getInt(1),resultSet.getString(2), resultSet.getString(3), resultSet.getInt(4)));
                }
            }catch (SQLException e){
                e.printStackTrace();
            }
        return dvdArray;
    }
}
```
{% endcapture %}
{% assign code_fence = code_fence | markdownify %}
{% include fix_linenos.html code=code_fence %}

---

## Класс DVDReturn (файл _DVDReturn.java_)

{% capture code_fence %}
```java
package sample.net.sqlitetutorial;

import java.util.ArrayList;

public class DVDReturn {
    int id;
    String titel;
    String director;
    int year;

    DVDReturn(int id, String titel, String director, int year){
        this.id = id;
        this.titel = titel;
        this.director = director;
        this.year = year;
    }

    public int getId(){
    	return this.id;
	}

    public String getTitel(){
		return this.titel;
	}

    public String getDirector(){
		return this.director;
	}

    public int getYear(){
		return this.year;
	}

    public void setId(int id){
		this.id = id;
	}

    public void setTitel(String titel){
		this.titel = titel;
	}

    public void setDirector(String director){
		this.director = director;
	}

    public void setYear(int year){
		this.year = year;
	}
}
```
{% endcapture %}
{% assign code_fence = code_fence | markdownify %}
{% include fix_linenos.html code=code_fence %}
