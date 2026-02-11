---
creation date: 2025-02-22 14:23
modification date: Saturday, 22nd February 2025
tags:
  - programming
  - java
note type: Informational Note
---
Basically it means that:
- We have a **class** that **depends on** other class/interface/whatever (does not work without it)
- If we want this class to work, we need to inject this dependency
- To make it follow a low coupling structure we create an **Injector class**
- This class is gonna inject this dependency, to make it possible we need to allow it in the constructor of the class where we inject the dependency
	
- This structure can be inherited (the dependency can get injected in any layer - subclass, subsubclass, etc.) 

*The code example*:
```java
// Service interface - defines the contract
public interface MessageService {
    void sendMessage(String message, String receiver);
}

// Implementation of service
public class EmailService implements MessageService {
    public void sendMessage(String message, String receiver) {
        System.out.println("Email sent to " + receiver + " with message: " + message);
    }
}

// Client class that depends on MessageService
public class MyApplication {
    private MessageService service;

    // Dependency is injected via constructor
    public MyApplication(MessageService service) {
        this.service = service;
    }

    public void processMessages(String msg, String rec) {
        // Delegate message sending to the injected service
        service.sendMessage(msg, rec);
    }
}

// Injector class responsible for creating and injecting dependencies
public class MessageServiceInjector {
    public static void main(String[] args) {
        // Create the service implementation
        MessageService emailService = new EmailService();

        // Inject the service into the client
        MyApplication app = new MyApplication(emailService);

        // Use the client class
        app.processMessages("Hello Dependency Injection", "user@example.com");
    }
}
```