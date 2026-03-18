**The core idea**: users paste text, get a short unique URL, and the paste expires after a configurable time. Simple on the surface, but technically rich underneath.

---
## Architecture Overview

| Layer          | Technology                   |
| -------------- | ---------------------------- |
| Backend        | Spring Boot 3, Java 21       |
| API            | GraphQL (Spring for GraphQL) |
| Database       | PostgreSQL                   |
| Cache          | Redis                        |
| Object Storage | MinIO (local S3 equivalent)  |
| Frontend       | Svelte 5 + TypeScript        |
| Build          | Maven                        |
| DB migrations  | flyway                       |

---
## Backend — Spring Boot
## Key Generation Service

Implement a `KeyGeneratorService` that runs on startup and on a schedule (e.g. `@Scheduled`) to pre-generate base62 hashes from a PostgreSQL sequence — exactly as the author describes. The main service just picks the next available key from the pool. This avoids hash collision logic at request time.

## Paste Service

- `createPaste(input)` → upload text to MinIO, save metadata to PostgreSQL, pop a key from the pool, return the short URL
    
- `getPaste(hash)` → check Redis cache first, fall back to PostgreSQL + MinIO fetch, increment `viewCount`
    
- `deletePaste(hash)` → soft or hard delete
    
- Scheduled job (`@Scheduled`) to delete expired pastes and purge MinIO objects
    

## GraphQL

Use `@QueryMapping` and `@MutationMapping` annotations from `spring-graphql`. Add `graphiql` enabled in `application.yml` for easy testing.

## Redis Caching

- Cache popular paste metadata with `@Cacheable("pastes")` using the hash as key
- Set TTL on cache entries matching paste `expiresAt`
- Use `spring-boot-starter-data-redis` + Lettuce

## Storage

- Use MinIO with the official `minio` Java SDK or AWS SDK S3 client pointed to MinIO
- Store paste content as plain `.txt` objects; key = paste hash

---

## Frontend — Svelte + TypeScript

## Pages

- `/` — Create paste form (textarea, optional title, TTL selector)
- `/[hash]` — View paste page (renders content, shows expiry, copy-link button)
- `/404` — Expired or not found

## GraphQL Client

Use `graphql-request` or `urql` for typed GraphQL calls. Define TypeScript types matching your schema. Example:

## UI Features

- Syntax highlighting with `highlight.js` (detect language automatically)
- Copy URL to clipboard button
- Countdown timer showing time remaining before expiry
- Character/byte counter (warn when approaching 10 MB)

---

## Additional Features to Practice

These go beyond the basics but are great for your skill set:

- **User auth with JWT** — Spring Security + JWT filter, store `ownerId` on pastes, let users see their paste history (good `SecurityFilterChain` practice)
- **Paste visibility** — `PUBLIC` / `UNLISTED` / `PRIVATE` enum; private pastes require auth (good for learning Spring Security method-level security with `@PreAuthorize`)
- **GraphQL Subscriptions** — Live view count updates using `Subscription` type and websockets in Spring for GraphQL
- **Flyway migrations** — manage your schema evolution (you already know this from work)
- **Rate limiting** — Use `Bucket4j` with Redis to limit paste creation per IP (great real-world pattern)
- **Pagination** — `getUserPastes(page, size): PastePage` query to practice GraphQL cursor/offset pagination

---

## Suggested Implementation Order

1. PostgreSQL schema + Flyway migrations
    
2. MinIO setup (Docker Compose)
    
3. Key generation service + pool table
    
4. `PasteService` with MinIO + PostgreSQL (no cache yet)
    
5. GraphQL schema + resolvers
    
6. Redis caching layer
    
7. Expiry scheduled job
    
8. Svelte frontend (create → view flow)
    
9. Auth (JWT) + paste ownership
    
10. Rate limiting + extra features
    
