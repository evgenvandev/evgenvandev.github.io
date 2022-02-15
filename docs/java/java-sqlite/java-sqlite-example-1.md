---
layout: default
title: Руководство SQLite Java
parent: Java and SQLite
grand_parent: Java
nav_order: 5
has_toc: false
---

# Руководство SQLite Java
{: .no_toc }
Здесь мы узнаем, как использовать SQLite в языке программирования JAVA для подключения базы данных SQLite, операций CREATE Table, 
INSERT, UPDATE, DELETE и SELECT для таблиц SQLite с использованием драйвера JDBC с примерами.

## Оглавление
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## Java интерфейс SQLite

[Ссылка на источник](https://www.tutlane.com/tutorial/sqlite/sqlite-java-tutorial)

Мы можем легко взаимодействовать с SQLite на языке JAVA, используя драйвер JDBC. Этот драйвер JDBC известен как пакет SQLite-JDBC, 
который содержит классы JAVA и библиотеки SQLite для выполнения различных операций, таких как подключение к базе данных, создание таблиц, 
вставка данных в таблицы и т.д. На платформе Windows, Linux и Mac OS.

Прежде чем мы приступим к взаимодействию с SQLite с использованием языка JAVA, сначала нам нужно убедиться, что установка JAVA доступна 
на нашем ПК. В случае, если установка JAVA недоступна, следуйте руководству Java по установке JAVA.

Если установка JAVA доступна на нашем ПК, теперь мы установим драйвер SQLite-JDBC для этого загрузите последнюю версию драйвера JDBC 
_sqlite-jdbc-version.jar_ из доступного списка драйверов JDBC.

Теперь нам нужно добавить загруженный файл jar драйвера JDBC (_sqlite-jdbc-version.jar_) в наш путь к классам, как показано в наших следующих программах.

## Подключиться к базе данных SQLite с помощью Java

Теперь мы подключимся к базе данных SQLite с помощью JAVA, если она существует, в противном случае она создаст новую базу данных, а затем подключится к ней.

Ниже приводится программа JAVA, которая используется для подключения к базе данных, если она существует, в противном случае она сначала 
создаст базу данных, а затем подключится к ней.

_Файл DBUsingJava.java_
```java
import java.sql.*;

public class DBUsingJava {
    public static void main(String args[]) {
        Connection c = null;
        try {
            Class.forName("org.sqlite.JDBC");
            c = DriverManager.getConnection("jdbc:sqlite:SqliteJavaDB.db");
        } catch (Exception e) {
            System.err.println(e.getClass().getName() + ": " + e.getMessage());
            System.exit(0);
        }
        System.out.println("database successfully created");
    }
}
```

Приведенный выше код пытается подключить базу данных _SqliteJavaDB.db_, если она существует, иначе он создаст новую базу данных по текущему 
пути, и мы предполагаем, что файл драйвера SQLite _sqlite-jdbc-3.8.11.2.jar_ доступен в том же месте, где существует наша программа.

```
javac DBUsingJava.java
java -classpath ".;sqlite-jdbs-3.8.11.2.jar" SQLiteJDBC

database successfully created
```

Вышеупомянутые операторы скомпилируют и запустят нашу программу для создания файла базы данных _SqliteJavaDB.db_ в текущем каталоге. 
Если проверить текущий каталог программы, то увидим, что создан один файл с именем _SqliteJavaDB.db_.

---

## Создание таблицы в SQLite используя Java

Теперь создадим новую таблицу в ранее созданной базе данных с именем _SqliteJavaDB.db_, используя java, для этого напишите код, как показано ниже.

_Файл TableUsingJava.java_
```java
import java.sql.*;

public class TableUsingJava {
    public static void main(String args[]) {
        Connection c = null;
        Statement stmt = null;
        
        try {
            Class.forName("org.sqlite.JDBC");
            c = DriverManager.getConnection("jdbc:sqlite:SqliteJavaDB.db");
            System.out.println("Database Opened...\n");
            stmt = c.createStatement();
            String sql = "CREATE TABLE Product " +
                "(p_id INTEGER PRIMARY KEY AUTOINCREMENT, " +
                "p_name TEXT NOT NULL, " +
                "price REAL NOT NULL, " +
                "quantity INTEGER)";
            stmt.executeUpdate(sql);
            stmt.close();
            c.close();
        } catch (Exception e) {
            System.err.println(e.getClass().getName() + ": " + e.getMessage());
            System.exit(0);
        }
        System.out.println("Table Product Created Successfully!!!");
    }
}
```

Приведённый выше код создаёт новую таблицу под названием _"Product"_ в базе данных _SqliteJavaDB.db_.
Теперь скомпилируем и запустим программу, используя следующие команды.

```
javac TableUsingJava.java
java -classpath ".;sqlite-jdbc-3.8.11.2.jar" TableUsingJava
Database Opened...

Table Product Created Successfully!!!
```

Приведённые выше операторы скомпилируют и запустят нашу программу, которая создаст таблицу _"Product"_ в нашей базе данных.

## DML операции (Insert, Select, Update, Delete) используя Java

Теперь мы попытаемся выполнить операции DML (insert, select, update, delete) над ранее созданной таблицей с именем Product, используя язык JAVA.

Следующая программа содержит все 4 операции DML, такие как INSERT, UPDATE, DELETE и SELECT.

```java
import java.util.Scanner;
import java.sql.*;

public class OperationUsingJava {
    public static void main(String args[]) {
        String flag = "Y";
        
        do {
            System.out.println("Select DML Operation For Product Table...");
            System.out.println("1. Insert");
            System.out.println("2. Update");
            System.out.println("3. Delete");
            System.out.println("4. Select");
            System.out.println("5. Exit");
            Scanner reader = new Scanner(System.in);
            System.out.println("Enter a choice: ");
            int n = reader.nextInt();
            Connection c = null;
            Statement stmt = null;
            try {
                Class.forName("org.sqlite.JDBC");
                c = DriverManager.getConnection("jdbc:sqlite:SqliteJavaDB.db");
                c.setAutoCommit(false);
                stmt = c.createStatement();
                String name = "", sql = "";
                float price = 0.0f;
                int quantity = 0;
                int id;
                Scanner scanName;
                switch(n) {
                    case 1:
                        scanName = new Scanner(System.in);
                        System.out.println("Enter Product Name:");
                        name = scanName.nextLine();
                        System.out.println("Enter Product Price:");
                        price = scanName.nextFloat();
                        System.out.println("Enter Product Quantity:");
                        quantity = scanName.nextInt();
                        sql = "INSERT INTO Product (p_name, price, quantity) " + 
                                "VALUES ('" + name + "'," + 
                                price + "," + quantity + ")";
                        stmt.executeUpdate(sql);
                        System.out.println("Inserted Successfully!!!");
                        break;

                    case 2:
                        scanName = new Scanner(System.in);
                        System.out.println("Enter Product id:");
                        id = scanName.nextInt();
                        System.out.println("Enter Product Name:");
                        scanName = new Scanner(System.in);
                        name = scanName.nextLine();
                        System.out.println("Enter Product Price:");
                        price = scanName.nextFloat();
                        System.out.println("Enter Product Quantity:");
                        quantity = scanName.nextInt();
                        sql = "UPDATE Product SET p_name = '" + name + "', price = " + price + 
                                ", quantity = " + quantity + " WHERE p_id = " + id;
                        stmt.executeUpdate(sql);
                        System.out.println("Update Successfully!!!");
                        break;

                    case 3:
                        scanName = new Scanner(System.in);
                        System.out.println("Enter Product id:");
                        id = scanName.nextInt();
                        sql = "DELETE FROM Product WHERE p_id = " + id + ";";
                        stmt.executeUpdate(sql);
                        System.out.println("Delete Successfully!!!!");
                        break;

                    case 4:
                        ResultSet rs = stmt.executeQuery("SELECT * FROM Product;");
                        System.out.println("ID\t Name\t\t Price\t Qty ");
                        while (rs.next()) {
                            id = rs.getInt("p_id");
                            name = rs.getString("p_name");
                            quantity = rs.getInt("quantity");
                            price = rs.getFloat("price");
                            System.out.println(id + "\t " + name + " \t " + price + "\t " + quantity);
                        }
                        rs.close();
                        break;

                    case 5:
                        System.exit(0);
                        break;

                    default:
                        System.out.println("Oops!!! Wrong Choice...");
                        break;
                }
                stmt.close();
                c.commit();
                c.close();
            } catch (Exception e) {
                System.err.println(e.getClass().getName() + ": " + e.getMessage());
                System.exit(0);
            }
            
            System.out.println("Continue Y OR N?");
            reader = new Scanner(System.in);
            flag = reader.nextLine();
            
        } while (flag.equalsIgnoreCase("Y"));
        System.exit(0);
    }
}
```

Приведённая выше программа выполняет операции INSERT, UPDATE, DELETE и SELECT в таблице _"Product"_.
Теперь скомпилируем и запустим программу, чтобы проверить результат, как показано ниже.

```
javac OperationUsingJava.java
java -classpath ".;sqlite-jdbc-3.8.11.2.jar" OperationUsingJava

Select DML Operation For Product Table...
1. Insert
2. Update
3. Delete
4. Select
5. Exit

Enter a choice:
1

Enter Product Name:
Pencil
Enter Product Price:
5
Enter Product Quantity:
50

Inserted Successfully!!!

Continue Y OR N?
Y

Select DML Operation For Product Table...
1. Insert
2. Update
3. Delete
4. Select
5. Exit

Enter a choice:
4

ID Name Price Qty
---- ------ ----- ----
1 Pencil 5.0 50

Continue Y OR N?
Y

Select DML Operation For Product Table...
1. Insert
2. Update
3. Delete
4. Select
5. Exit

Enter a choice:
2

Enter Product id:
1
Enter Product Name:
Sharpner
Enter Product Price:
10
Enter Product Quantity:
90

Updated Successfully!!!

Continue Y OR N?
Y

Select DML Operation For Product Table...
1. Insert
2. Update
3. Delete
4. Select
5. Exit

Enter a choice:
4

ID Name Price Qty
---- -------- ----- ----
1 Sharpner 10.0 90

Continue Y OR N?
Y

Select DML Operation For Product Table...
1. Insert
2. Update
3. Delete
4. Select
5. Exit

Enter a choice:
1

Enter Product Name:
Scale
Enter Product Price:
5
Enter Product Quantity:
60

Inserted Successfully!!!

Continue Y OR N?
Y

Select DML Operation For Product Table...
1. Insert
2. Update
3. Delete
4. Select
5. Exit

Enter a choice:
4

ID Name Price Qty
---- -------- ---- ---
1 Sharpner 10.0 90
2 Scale 5.0 60

Continue Y OR N?
Y

Select DML Operation For Product Table...
1. Insert
2. Update
3. Delete
4. Select
5. Exit

Enter a choice:
3

Enter Product id:
2

Deleted Successfully!!!

Continue Y OR N?
y

Select DML Operation For Product Table...
1. Insert
2. Update
3. Delete
4. Select
5. Exit

Enter a choice:
4

ID Name Price Qty
---- -------- ----- ----
1 Sharpner 10.0 90

Continue Y OR N?
n
```

Вот так мы можем использовать базу данных SQLite в JAVA для выполнения операций INSERT, UPDATE, DELETE 
и SELECT в соответствии с нашими требованиями.
