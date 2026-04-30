**OpenSSL** <mark style="background:rgba(205, 244, 105, 0.55)">FIXED</mark> (almost)
- Issue 1 `CVE-2026-28390` — OpenSSL NULL pointer dereference in CMS EnvelopedData (KeyTransport), DoS
    
- Issue 8 `CVE-2026-31790` — OpenSSL RSASVE key encapsulation leaks uninitialized memory to remote peer
    
- Issue 9 `CVE-2026-2673` — OpenSSL TLS 1.3 server negotiates wrong key exchange group with `DEFAULT` keyword
    
- Issue 13 `CVE-2026-28389` — OpenSSL NULL pointer dereference in CMS EnvelopedData (KeyAgree), DoS
    
- Issue 15 `CVE-2025-69419` — OpenSSL off-by-one heap write in `PKCS12_get_friendlyname()` with non-ASCII BMPString
    
- Issue 21 `CVE-2025-69420` — OpenSSL type confusion in TimeStamp Response verification, NULL pointer dereference
    
- Issue 26 `CVE-2025-15467` — OpenSSL stack buffer overflow parsing CMS AuthEnvelopedData with crafted AEAD params (score 8.8)
    
- Issue 84 `CVE-2026-28388` — OpenSSL NULL pointer dereference when processing delta CRL missing CRL Number extension
    
- Issue 251 `CVE-2025-69421` — OpenSSL NULL pointer dereference in `PKCS12_item_decrypt_d2i_ex()` on malformed PKCS#12

Issues 8, 9, 13, 84 - <mark style="background:rgba(205, 244, 105, 0.55)">fix by triggering the pipeline (package auto updates)</mark>
Issues 1, 15, 21, 26, 251 - `apt-get install -y --only-upgrade openssl libssl-dev` <mark style="background:rgba(205, 244, 105, 0.55)">in front Dockefile</mark>

**Node.js Runtime** <mark style="background:#d4b106">REVIEW</mark>
- *Issue 3* `CVE-2026-21710` — Node.js HTTP server crashes on `__proto__` header when accessing `req.headersDistinct` - <mark style="background:rgba(205, 244, 105, 0.55)">switch to node v25.8.2</mark>
    
- *Issue 133* `CVE-2026-21637` — Node.js TLS server crash/FD leak when `pskCallback` or `ALPNCallback` throw synchronously - <mark style="background:rgba(205, 244, 105, 0.55)">switch to node v25.8.2</mark>

**Apache HTTP Server**
- Issue 6 `CVE-2025-58098` — Apache httpd ≤2.4.65 SSI `#exec cmd` receives shell-escaped query string (score 8.3)
    
- Issue 73 `CVE-2025-55753` — Apache httpd ACME renewal integer overflow leads to infinite retry loop

**OS Libraries**
- Issue 4 `CVE-2026-22184` — zlib buffer overflow in standalone `untgz` utility via long archive name
    
- Issue 5 `CVE-2026-40200` — musl libc stack corruption in `qsort` on very large arrays (score 8.1)
    
- Issue 18 `CVE-2024-57795` — Linux kernel vulnerability in `linux-libc-dev` (Ubuntu 24.04)
    
- Issue 27 `CVE-2026-23111` — Linux kernel vulnerability in `linux-image-aws` (Ubuntu 24.04)
    
- Issue 278 `CVE-2025-68263` — Linux kernel vulnerability in `linux-image-aws`, score 8.4
    
- Issue 241 `CVE-2025-22022` — Linux kernel vulnerability in `linux-libc-dev` (Ubuntu 24.04)
    
- Issue 293 `CVE-2025-62626` — AMD CPU RDSEED insufficient entropy, local attacker can influence random values (score 10)

**Spring Framework / Boot (dev-back)**
- Issue 29 `CVE-2024-22243` — Spring `UriComponentsBuilder` open redirect / SSRF via external URL (score 8.1)
    
- Issue 46 `CVE-2024-22262` — Spring `UriComponentsBuilder` SSRF/redirect bypass follow-up (score 8.1)
    
- Issue 83 `CVE-2024-22259` — Spring `UriComponentsBuilder` SSRF/redirect (score 8.1)
    
- Issue 47 `CVE-2024-38816` — Spring WebMvc path traversal via static resource serving — **exploit available** (score 7.5)
    
- Issue 51 `CVE-2024-38819` — Spring WebMvc path traversal via functional web framework static resources
    
- Issue 40 `CVE-2025-41249` — Spring annotation resolution failure in parameterized type hierarchies, may bypass authorization
    
- Issue 48 `CVE-2025-22235` — Spring Boot `EndpointRequest.to()` creates `null/**` matcher for disabled actuator endpoints

**Netty (dev-back)** <mark style="background:rgba(205, 244, 105, 0.55)">FIXED</mark>
- Issue 24 `CVE-2026-33871` — Netty HTTP/2 DoS via flood of zero-byte `CONTINUATION` frames (score 7.5) <mark style="background:rgba(205, 244, 105, 0.55)">FIXED</mark> (version 4.1.132.Final)
    
- Issue 60 `CVE-2025-58057` — Netty BrotliDecoder unbounded buffer allocation leads to OOM DoS <mark style="background:rgba(205, 244, 105, 0.55)">FIXED</mark> in Issue 24
    
- Issue 187 `CVE-2025-55163` — Netty HTTP/2 "MadeYouReset" DDoS via malformed control frames breaking stream limits <mark style="background:rgba(205, 244, 105, 0.55)">FIXED</mark> in Issue 24
    
- Issue 112 `GHSA-xpw8-rcwv-8f8p` — Netty HTTP/2 RST frame flood causing excessive server load / DDoS <mark style="background:rgba(205, 244, 105, 0.55)">FIXED</mark> in Issue 24
    
- Issue 208 `CVE-2025-24970` — Netty SslHandler native crash on specially crafted packet 
	<mark style="background:rgba(205, 244, 105, 0.55)">FIXED</mark> in Issue 24

**Logback (dev-back)**
- Issue 25 `CVE-2023-6378` — Logback receiver deserialization DoS via poisoned data (v1.4.11)
    
- Issue 52 `CVE-2023-6481` — Logback receiver deserialization DoS follow-up (v1.4.13/1.3.13/1.2.12)

**Jetty (dev-back)**
- Issue 19 `CVE-2024-13009` — Jetty buffer corruption and data sharing between requests on gzip inflate error
    
- Issue 78 `CVE-2024-9823` — Jetty DosFilter OOM via repeated crafted requests
    
- Issue 45 `CVE-2026-2332` — Jetty HTTP/1.1 request smuggling via chunk extensions

**Node.js npm Packages (dev-front)**
- Issue 2 `CVE-2026-33671` — picomatch ReDoS via crafted extglob `+()` / `*()` patterns 
	<mark style="background:rgba(205, 244, 105, 0.55)">FIXED</mark> (-> v4.0.4)
    
- Issue 10 `CVE-2026-2229` — undici WebSocket DoS via invalid `server_max_window_bits` causing `RangeError` <mark style="background:rgba(205, 244, 105, 0.55)">FIXED</mark> (in crit vlbs)
    
- Issue 101 `CVE-2026-1528` — undici WebSocket DoS via 64-bit frame length overflow in `ByteParser` <mark style="background:rgba(205, 244, 105, 0.55)">FIXED</mark> (in crit vlbs)
    
- Issue 115 `CVE-2026-1526` — undici WebSocket decompression bomb via unbounded permessage-deflate inflation <mark style="background:rgba(205, 244, 105, 0.55)">FIXED</mark> (in crit vlbs)
    
- Issue 14 `CVE-2026-26996` — minimatch ReDoS via consecutive `*` wildcards, O(4^N) complexity <mark style="background:rgba(205, 244, 105, 0.55)">FIXED</mark> (-> v10.2.3)
    
- Issue 22 `CVE-2026-27904` — minimatch ReDoS via nested `*()` extglobs producing catastrophic backtracking <mark style="background:rgba(205, 244, 105, 0.55)">FIXED</mark> (-> v10.2.3)
    
- Issue 33 `CVE-2026-33891` — node-forge DoS via infinite loop in `BigInteger.modInverse()` with zero input  <mark style="background:rgba(205, 244, 105, 0.55)">FIXED</mark> (in crit vlbs)
    
- Issue 30 `CVE-2026-34043` — serialize-javascript DoS via array-like object with huge `length` property <mark style="background:rgba(205, 244, 105, 0.55)">FIXED</mark> (-> v7.0.5)
    
- Issue 32 `GHSA-5c6j-r48x-rmvq` — serialize-javascript XSS / code injection vulnerability
	<mark style="background:rgba(205, 244, 105, 0.55)">FIXED</mark> (-> v7.0.5)
    
- Issue 28 `CVE-2026-4867` — path-to-regexp ReDoS or routing bypass vulnerability <mark style="background:rgba(205, 244, 105, 0.55)">FIXED</mark> (-> v0.1.13) 
    
- Issue 127 `CVE-2026-32141` — flatted stack overflow crash via deeply nested circular JSON payload <mark style="background:rgba(205, 244, 105, 0.55)">FIXED</mark> (in crit vlbs)
    
- Issue 36 `CVE-2026-2391` — `qs` library `arrayLimit` bypass with `comma: true`, memory exhaustion DoS <mark style="background:rgba(205, 244, 105, 0.55)">FIXED</mark> (-> v6.14.2)
    
- Issue 41 `CVE-2026-26960` — node-tar hardlink escape during extraction allows arbitrary file read/write <mark style="background:#9254de">NNTF</mark> (probably will be fixed by the maintainers of Docker image)
    
- Issue 100 `CVE-2026-29074` — SVGO XML entity expansion / recursion causes heap OOM crash <mark style="background:rgba(205, 244, 105, 0.55)">FIXED</mark> (-> v4.0.1)
    
- Issue 258 `CVE-2026-29063` — immutable.js prototype pollution via `mergeDeep`, `merge`, `Map.toJS` <mark style="background:rgba(205, 244, 105, 0.55)">FIXED</mark> (in crit vlbs)
    
- Issue 61 `CVE-2026-33151` — socket.io-parser issue <mark style="background:rgba(205, 244, 105, 0.55)">FIXED</mark> (-> v4.2.6)

**Linux Kernel / EC2**
- Issue 524 `CVE-2026-23074` — Linux kernel vulnerability (Ubuntu 24.04 / EC2)
    
- Issue 761 `CVE-2026-34982` — Linux kernel vulnerability (Ubuntu 24.04 / EC2)
    
- Issue 381 `CVE-2025-38022` — Linux kernel vulnerability (Ubuntu 24.04 / EC2)
    
- Issue 136 `CVE-2026-24842` — Linux kernel vulnerability (Ubuntu 24.04 / EC2)
    
- Issue 145 `CVE-2026-27903` — Linux kernel vulnerability (Ubuntu 24.04 / EC2)
    
- Issue 150 `CVE-2025-69873` — Linux kernel vulnerability (Ubuntu 24.04 / EC2)
    
- Issue 168 `CVE-2026-33894` — Linux kernel vulnerability (Ubuntu 24.04 / EC2)



# NNTF - No Need To Fix