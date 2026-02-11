---
creation date: 2025-02-22 14:23
modification date: Saturday, 22nd February 2025
tags:
  - programming
  - patterns
note type: Informational Note
---
This is a Second pattern described in [[Design patterns]] book.

# Definition
Паттерн Наблюдатель определяет отношение «**один ко многим**» между объектами таким образом, что при изменении состояния одного объекта происходит автоматическое оповещение и обновление всех зависимых объектов.

---
## How does it work?

1. There is a publisher that started to sell his newspapers.
2. You subscribe to this publisher and every time a new newspaper is published, it gets sent to you. Until subscription is active.
3. If you don't want to get this newspaper anymore, you cancel the subscription.
4. Until the newspaper continues publishing, persons, hotels, and others keep subscribing and canceling the subscription.

**Basic formula**:
Publishers + Subscribers = Observer Pattern

![[Pasted image 20250814182240.png]]

Object `Duck` can be added to Observers, by requesting. 
Also, any observer can stop being observer, also by requesting.

---

This pattern tends to a **low coupling**. Because this approach helps with maintaining a program, reduces the number of errors.