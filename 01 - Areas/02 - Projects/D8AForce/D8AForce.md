- null pointer fix 
```java
java.lang.NullPointerException
	at java.time.Duration.between(Duration.java:473)
	at com.d8aforce.infrastructure.mail.MailMessagesBuilder.getDuration(MailMessagesBuilder.java:222)
	at com.d8aforce.infrastructure.mail.MailMessagesBuilder.buildS3ProcessEmail(MailMessagesBuilder.java:121)
	at com.d8aforce.server.scheduler.MailScheduler.lambda$sendS3ProcessEmail$0(MailScheduler.java:117)
	at java.util.ArrayList.forEach(ArrayList.java:1257)
	at com.d8aforce.server.scheduler.MailScheduler.sendS3ProcessEmail(MailScheduler.java:116)
	at com.d8aforce.server.scheduler.MailScheduler$$FastClassBySpringCGLIB$$efd66709.invoke(<generated>)
	at org.springframework.cglib.proxy.MethodProxy.invoke(MethodProxy.java:218)
```

