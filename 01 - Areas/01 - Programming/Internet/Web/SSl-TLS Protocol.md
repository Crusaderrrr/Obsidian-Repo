**SSL is technically deprecated**. What everyone calls **"SSL" today is actually TLS** (Transport Layer Security), its successor. SSL 3.0 was retired in 2015 due to vulnerabilities. The name just stuck.

#### Key traits:
- Sits between **Transport** and **Application** layers, right in **Session** layer. (see [[OSI model]]) 
- It takes raw TCP connection and wraps it in the encryption before getting to the application 

#### The basic flow:
1. TCP connection established 
2. TLS handshake 
3. encrypted tunnel 
4. HTTP runs through that tunnel.