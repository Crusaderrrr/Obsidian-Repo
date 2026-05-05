This is a **behavioral pattern** that *turns a request into a standalone object* containing all information about that request, letting us execute the same request from all over the app.

Imagine ordering food at a restaurant.
1. **You (Client)**: You look at the menu and decide what you want.
2. **The Waiter (Invoker)**: You give your order to the waiter. The waiter writes it on a piece of paper. The waiter doesn't need to know how to cook the food; they just know how to take the order and pass it to the kitchen.
3. **The Order (Command)**: The piece of paper has all the details of the request.
4. **The Chef (Receiver)**: The chef reads the order and knows exactly how to prepare the meal.

## Basic implementation
1. *The command interface*
```java
public interface Command { 
	void execute(); 
}
```

2. *The receiver*
```java
public class Light {
    public void turnOn() {
        System.out.println("The light is ON");
    }

    public void turnOff() {
        System.out.println("The light is OFF");
    }
}
```

3. *Concrete commands*
```java
public class LightOnCommand implements Command {
    private Light light;

    public LightOnCommand(Light light) {
        this.light = light;
    }

    @Override
    public void execute() {
        light.turnOn();
    }
}

public class LightOffCommand implements Command {
    private Light light;

    public LightOffCommand(Light light) {
        this.light = light;
    }

    @Override
    public void execute() {
        light.turnOff();
    }
}
```

4. *The invoker*
```java
public class RemoteControl {
    private Command command;

    // Set the command you want to execute
    public void setCommand(Command command) {
        this.command = command;
    }

    // Press the button on the remote
    public void pressButton() {
        command.execute();
    }
}
```

5. *The client*
```java
public class SmartHomeApp {
    public static void main(String[] args) {
        // 1. Create the Receiver
        Light livingRoomLight = new Light();

        // 2. Create the Concrete Commands
        Command lightOn = new LightOnCommand(livingRoomLight);
        Command lightOff = new LightOffCommand(livingRoomLight);

        // 3. Create the Invoker
        RemoteControl remote = new RemoteControl();

        // Turn the light ON
        remote.setCommand(lightOn);
        remote.pressButton(); 

        // Turn the light OFF
        remote.setCommand(lightOff);
        remote.pressButton(); 
    }
}
```