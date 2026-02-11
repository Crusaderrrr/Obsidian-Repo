---
creation date: 2025-02-22 14:23
modification date: Saturday, 22nd February 2025
tags:
  - programming
  - JavaScript
note type: Informational Note
---
This expression is used to describe how asynchronous programming was when Promises wasn't yet invented. 
So the API call part looked like that:
```JavaScript
getUser(userId, (user) => {
  getOrders(user, (orders) => {
    processOrders(orders, (processed) => {
      sendEmail(processed, (confirmation) => {
        console.log("Order Processed:", confirmation);
      });
    });
  });
});
```

These are *nested callback functions*. 

### The main problem
- Low maintainability 
- Low extensibility 
- Hard to read code