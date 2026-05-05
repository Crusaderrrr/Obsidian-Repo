This is a **creational pattern** that lets us create families of objects, basically it is a *factory of factories*.

**Imagine**, we have a UI framework that lets us create buttons, scrollbars, etc. and it should work on both Windows and Mac. In that case we could use this pattern to define an abstract class of a factory, and a classes like `WindowsFactory` and `MacFactory` that extend it.

## Example

1. *Abstract products*
```java
public interface Button {
    void paint();
}

public interface Checkbox {
    void paint();
}
```

2. *Concrete product*
```java
// Windows family
public class WindowsButton implements Button {
    @Override
    public void paint() {
        System.out.println("Rendering a button in Windows style.");
    }
}

public class WindowsCheckbox implements Checkbox {
    @Override
    public void paint() {
        System.out.println("Rendering a checkbox in Windows style.");
    }
}

// macOS family
public class MacButton implements Button {
    @Override
    public void paint() {
        System.out.println("Rendering a button in macOS style.");
    }
}

public class MacCheckbox implements Checkbox {
    @Override
    public void paint() {
        System.out.println("Rendering a checkbox in macOS style.");
    }
}
```

3. *Abstract Factory*
```java
public interface GUIFactory {
    Button createButton();
    Checkbox createCheckbox();
}
```

4. *Concrete factories*
```java
public class WindowsFactory implements GUIFactory {
    @Override
    public Button createButton() {
        return new WindowsButton();
    }

    @Override
    public Checkbox createCheckbox() {
        return new WindowsCheckbox();
    }
}

public class MacFactory implements GUIFactory {
    @Override
    public Button createButton() {
        return new MacButton();
    }

    @Override
    public Checkbox createCheckbox() {
        return new MacCheckbox();
    }
}
```