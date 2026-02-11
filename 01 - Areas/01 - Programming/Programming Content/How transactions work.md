---
creation date: 2025-02-22 14:23
modification date: Saturday, 22nd February 2025
tags:
  - programming
note type: Informational Note
---
There are **5 main parts** of all the transactions:
1. *Cardholder* 
2. *Merchant* - how accepts the payment 
3. *Acquiring bank* (Acquire) - The merchant's bank 
4. *Issuing bank* (Issuer) - The customer's bank
5. *Card Network* - Visa, Mastercard

There are **3 phases** of how transaction is going:
1. **Authorization**
	- Where the card data (number, CVV, etc. ) is captured and transmitted via *Card Network*, which routes the card request to *Issuing Bank*, where the balance is checked, card validity and other related stuff. 
	- After that the Issuing Bank sends the Approval or Decline response. 
	- If approved, the merchant can complete the sale.
2. **Clearing** 
	- Merchant don't process payments individually, instead they do it in batches.
	- All the payments are accumulated and processed, normally in the end of the day
	- The processor forwards transactions through card networks to respective issuing banks
	- The Issuing bank converts the *holds* -> into -> actual charges
3. **Settlement**
	- Card networks collect transactions funds 
	- Fees are deducted 
	- The network transfers remaining funds to the merchant's acquiring bank, minus additional fees
	- The acquiring bank deposits the funds into merchant's business account, minus processing fees
	- The Issuing bank adds the charge to the customer's monthly statement 


# Security
## 3D Secure Authentication
**3D Secure (3DS)** adds an extra authentication layer that verifies the cardholder's identity during online transactions. The "three domains" refer to the merchant, the card issuer, and the card network infrastructure connecting them.

Modern 3DS2 (also called EMV 3DS) analyzes over 100 data points including device information, purchase history, and behavioral patterns to determine risk level, reducing friction for legitimate customers while blocking fraudsters.


## PCI DSS Compliance

**PCI DSS (Payment Card Industry Data Security Standard)** is a comprehensive set of security requirements that all entities handling card data must follow. The standard includes 12 major requirements organized into six categories :
1. **Build and maintain secure networks** - firewalls, no passwords
2. **Protect cardholder data** - Encrypt stored data, mask card numbers when displayed
3. **Maintain vulnerability management** - Anti-virus software, secure coding practices
4. **Implement strong access controls** - Restrict data access on need-to-know basis, unique IDs for each person with access
5. **Regularly monitor and test networks** - Track all access to card data
6. **Maintain information security policy** - Written policies and procedures for all personnel


## Tokenization 
The simple token is used instead of a card number during transaction, so hackers cannot access it. This token is a unique string, that does not have any mathematical relation to the card number.