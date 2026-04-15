**Program to an interface, not an implementation**

This is how I interpret it:
You need to create interfaces that define *WHAT* it (implementation class) is doing, and the class implements *HOW* it is done. 

<font color="#c00000">IMPORTANT</font>: 
We can use Interface as the type if we want spring decide which interface to use, like that:
```java
@Bean  
public JavaMailSender getJavaMailSender() {  
    JavaMailSenderImpl mailSender = new JavaMailSenderImpl();
    ...
}
```
in that example Interface is used as return type, but the actual return is the class.

---

<mark style="background:#ff4d4f">How you don't do</mark>:
```java
// Your service is LOCKED to email forever
public class NotificationService {
    private SESEmailSender emailSender; // concrete class

    public void notify(String message) {
        emailSender.sendEmail(message);
    }
}
```
(concrete **class** is used here)



<mark style="background:#affad1">How you should do</mark>:
```java
// Define the contract — what a notifier must be able to do
public interface Notifier {
    void send(String message);
}

// Multiple implementations of the same contract
public class EmailNotifier implements Notifier {
    public void send(String message) {
        // send via AWS SES
    }
}

public class SMSNotifier implements Notifier {
    public void send(String message) {
        // send via SMS gateway
    }
}

// Service only knows about the contract, not WHO fulfills it
public class NotificationService {
    private final Notifier notifier; // interface type ✅

    public NotificationService(Notifier notifier) {
        this.notifier = notifier;
    }

    public void notify(String message) {
        notifier.send(message); // works with ANY Notifier
    }
}
```

There is an interface `Notifier` that defines WHAT are implementation classes do, but how they do it is their responsibility.

---

## Real cases
For example, we have many classes that implement an interface and in some places we need a concrete class's implementation. This is how we could manage this situation:

1. **Factory method**
```java
public class NotifierFactory {
    public static Notifier create(String type) {
        switch (type) {
            case "email": return new EmailNotifier();
            case "sms":   return new SMSNotifier();
            default: ...
        }
    }
}

// ----------------------------Usage--------------------------------------
public class NotificationService {
    public void notifyInvestor(String type, String message) {
        Notifier notifier = NotifierFactory.create(type); // pick here
        notifier.send(message);
    }
}

// calling it
notificationService.notifyInvestor("email", "You are classified as PRO");
notificationService.notifyInvestor("sms",   "You are classified as PRO");
```

2. **Pass the impl at construction time**
```java
// No factory needed — caller makes the choice
NotificationService emailService = new NotificationService(new EmailNotifier());
NotificationService smsService   = new NotificationService(new SMSNotifier());

// Then use each one where appropriate
emailService.notify("Investor classified as PRO");
smsService.notify("Investor classified as PRO");
```

3. **Map registry**
Similar to factory, but instead we simply define the `Map` that holds implementations, and we would need to add the new classes there:
```java
public class NotifierRegistry {
    private final Map<String, Notifier> registry = new HashMap<>();

    public NotifierRegistry() {
        registry.put("email", new EmailNotifier());
        registry.put("sms",   new SMSNotifier());
    }

    public Notifier get(String type) {
        Notifier notifier = registry.get(type);
        if (notifier == null) throw new IllegalArgumentException("No notifier for: " + type);
        return notifier;
    }
}

// Usage
NotifierRegistry registry = new NotifierRegistry();
registry.get("sms").send("Classified as GREY");
```