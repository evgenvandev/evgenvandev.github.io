---
layout: default
title: Перечисления в Java
parent: Enums in Java
grand_parent: Java
nav_order: 2
has_toc: false
---

# Перечисления в Java
{: .no_toc }

## Оглавление
{: .no_toc .text-delta }

1. TOC
{:toc}

---

Перечисления в Java могут также хранить собственные переменные и методы.  
Для этого надо создать _enum_ конструктор и добавить его вызов к значениям.  
Приведём пример:

### _Файл Directions.java_
```java
public enum Directions {
    EAST,
    WEST,
    NORTH,
    SOUTH
}
```

### _Файл Directions2.java_
```java
public enum Directions2 {
	EAST("E"),
	WEST("W"),
	NORTH("N"),
	SOUTH("S");
	private final String shortCode;
	
	Directions2(String code) {
		this.shortCode = code;
	}
	
	public String getDirectionCode() {
		return this.shortCode;
	}
}
```

### _Файл EnumExample.java_
```java
public class EnumExample {
    public static void main(String[] args) {
        Directions dir = Directions.EAST;
        System.out.println(dir);  // EAST
        
        Directions2 dir2 = Directions2.EAST;
        System.out.println(dir2.getDirectionCode());  // E
    }
}
```

