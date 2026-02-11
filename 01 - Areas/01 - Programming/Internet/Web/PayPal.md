---
creation date: 2025-02-22 14:23
modification date: Saturday, 22nd February 2025
tags:
  - programming
  - web
  - paypal
note type: Informational Note
---
This is how **PayPal workflow** looks like on transactions:

1. **Start Payment** (*Frontend -> Backend*)
	- The user clicks a PayPal button 
	- The user is redirected to the page where he should login to his account (authorization)
	- Then the <mark style="background: #D2B3FFA6;">POST request</mark> is sent to `/create-payment` to the backend with order details (amount, currency, etc.)
2. **Create Payment** (*Backend -> PayPal API*)
	- <mark style="background: #D2B3FFA6;">POST request</mark> PayPal API to checkout order. *Payload*: order amount, return/cancel URLs, Client ID in headers.
	- The money is held on this step for transaction.
	- Then we receive an `approvalUrl` and `orderId`, those are sent to Frontend
3. **User Approves** (*Frontend -> PayPal*)
	- The user is redirected to approval page of PayPal with order details, here he clicks *Pay Now*, PayPal then sends a response with query parameters like:
	  `?paymentId=ABC123&token=XYZ&PayerID=123ABC`
4. **Execute Payment** (*Frontend -> Backend*)
	- POST reques is sent from Frontend -> Backend to `/execute-payment`
	- The data from params is sent 
5. **Capture Funds** (*Backend -> PayPal*)
	- POST request to PayPal API (orderId, payerId and secret) to PayPal `../{orderId}/capture`.
	- This is where the money is really sent 
	- JSON with the status of the order is received back ('COMPLETE', other info)