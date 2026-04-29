This is **Chain of Responsibility pattern**.

The three key participants are:
- **Client** — builds the chain and triggers it by calling the first handler
- **Handler (abstract)** — defines the interface with a `handleRequest()` method and holds a reference to the next handler
- **ConcreteHandlers** — implement the actual logic; each either handles the request or delegates to `nextHandler`

## Example

*Handler base class*
```java
public abstract class SupportHandler {
    protected SupportHandler nextHandler;

    public SupportHandler setNext(SupportHandler next) {
        this.nextHandler = next;
        return next;
    }

    public abstract void handle(int severity);
}
```

*Concrete handlers*
```java
public class Level1Support extends SupportHandler {
    public void handle(int severity) {
        if (severity == 1) {
            System.out.println("Level 1 (Help Desk): Issue resolved.");
        } else if (nextHandler != null) {
            nextHandler.handle(severity);
        }
    }
}

public class Level2Support extends SupportHandler {
    public void handle(int severity) {
        if (severity == 2) {
            System.out.println("Level 2 (Tech Support): Issue resolved.");
        } else if (nextHandler != null) {
            nextHandler.handle(severity);
        }
    }
}

public class Level3Support extends SupportHandler {
    public void handle(int severity) {
        if (severity == 3) {
            System.out.println("Level 3 (Senior Engineer): Issue resolved.");
        } else if (nextHandler != null) {
            nextHandler.handle(severity);
        }
    }
}

public class Level4Support extends SupportHandler {
    public void handle(int severity) {
        if (severity == 4) {
            System.out.println("Level 4 (Engineering Manager): Issue escalated to management.");
        } else {
            System.out.println("Unhandled severity: " + severity + ". No handler available.");
        }
    }
}
```

*Usage*
```java
public class Main {
    public static void main(String[] args) {
        // Build the chain
        Level1Support l1 = new Level1Support();
        Level2Support l2 = new Level2Support();
        Level3Support l3 = new Level3Support();
        Level4Support l4 = new Level4Support();

        l1.setNext(l2).setNext(l3).setNext(l4);

        // Fire requests
        l1.handle(1); // Level 1 (Help Desk): Issue resolved.
        l1.handle(3); // Level 3 (Senior Engineer): Issue resolved.
        l1.handle(4); // Level 4 (Engineering Manager): Issue escalated to management.
        l1.handle(9); // Unhandled severity: 9. No handler available.
    }
}
```


> [!attention]
> **Severtiy** is a concrete task that one of the handlers can resolve. In the case of that example it is just a number.
 