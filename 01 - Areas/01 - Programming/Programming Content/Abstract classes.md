---
creation date: 2025-02-22 14:23
modification date: Saturday, 22nd February 2025
tags:
  - programming
  - oop
note type: Informational Note
---
## Что такое абстрактный класс?

**Абстрактный класс** — это класс, который объявлен с помощью специального ключевого слова ( `abstract`  в большинстве языков программирования). На его основе нельзя создать объект напрямую. Такой класс обычно служит шаблоном для других классов, определяя общий интерфейс и частичную реализацию для группы связанных классов-потомков. В абстрактном классе могут быть как методы с реализацией, так и абстрактные методы (без реализации), которые обязательно должны быть реализованы в дочерних классах.

- It is recommended to use `@Override` when implementing abstract methods in child classes.

**Пример на Java**
```java
abstract class Animal {
    abstract void makeSound(); // Абстрактный метод
    void sleep() { System.out.println("Zzz"); } // Обычный метод
}

class Dog extends Animal {
	@Override
    void makeSound() { System.out.println("Woof"); }
}

```