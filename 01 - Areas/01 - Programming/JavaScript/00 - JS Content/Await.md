---
creation date: 2025-02-22 14:23
modification date: Saturday, 22nd February 2025
tags:
  - JavaScript
  - programming
note type: Informational Note
---
 A **Promise** is an *object* representing the eventual completion (or failure) of an asynchronous operation. It has three states:
- *Pending*: The operation is in progress.
- *Fulfilled*: The operation completed successfully (resolved).
- *Rejected*: The operation failed (rejected).

**Async/Await**: A [syntactic sugar](https://www.lenovo.com/us/en/glossary/syntactic-sugar/) over Promises, making asynchronous code look synchronous and easier to manage.

A **Promise** is created using the Promise constructor or returned by many asynchronous APIs (like fetch). You handle its result using `.then()` for *success* and `.catch()` for *errors*.

*Promise Example*:
```JavaScript
// Fetching data from an API using Promises
fetch('https://jsonplaceholder.typicode.com/users')
  .then(response => {
    if (!response.ok) {
      throw new Error('Network response was not ok');
    }
    return response.json(); // Parse the response as JSON
  })
  .then(data => {
    console.log(data); // Array of users
  })
  .catch(error => {
    console.error('Error:', error);
  });
```

*Async/Await Example*:
```JavaScript
async function fetchUsers() {
  try {
    const response = await fetch('https://jsonplaceholder.typicode.com/users');
    if (!response.ok) {
      throw new Error('Network response was not ok');
    }
    const data = await response.json();
    console.log(data);
  } catch (error) {
    console.error('Error:', error);
  }
}

fetchUsers();
```