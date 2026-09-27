**Hash-based Message Authentication Code** this is a construction that combines a hash function with a secret key to provide both message integrity and and [[Authentication and Authorization||authentication]]. 

*Plain hashing* only tells us the data hasn't changed, *HMAC* also tells who sent it.

#### The problem it solves 
- When we send a message over an insecure internet someone can intercept it and change the contents. 
- In order to prevent that, we can compute an HMAC, based on the message, shared secret key and a hash function and attach it to the payload. 
- When the message comes to the destination, the receiver can take a message, and recompute its HMAC, if it matches, then the message was not corrupted.