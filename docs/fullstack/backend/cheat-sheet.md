# Backend Cheat Sheet

## HTTP methods

| Method | Use | Idempotent | Body |
|---|---|---|---|
| GET | Read | Yes | No |
| POST | Create | No | Yes |
| PUT | Replace | Yes | Yes |
| PATCH | Partial update | No | Yes |
| DELETE | Delete | Yes | Optional |

## Status codes

| Code | Meaning |
|---|---|
| 200 | OK |
| 201 | Created |
| 204 | No Content |
| 301 / 302 | Moved permanently / temporarily |
| 304 | Not Modified (cache) |
| 400 | Bad Request |
| 401 | Unauthorized (not logged in) |
| 403 | Forbidden (no permission) |
| 404 | Not Found |
| 409 | Conflict |
| 422 | Validation error |
| 429 | Too Many Requests |
| 500 | Server error |
| 502 / 503 / 504 | Bad gateway / unavailable / timeout |

## REST URL design

```text
GET    /users            list
GET    /users/42         one
POST   /users            create
PUT    /users/42         replace
PATCH  /users/42         update fields
DELETE /users/42         delete
GET    /users/42/orders  nested
GET    /users?page=2&limit=20&sort=-created_at
```

Rules: plural nouns, no verbs, lowercase, hyphens.

## curl

```bash
curl https://api.example.com/users
curl -i URL                                   # show headers
curl -X POST URL -H "Content-Type: application/json" -d '{"name":"a"}'
curl -H "Authorization: Bearer <token>" URL
curl -o file.zip URL                          # save
curl -L URL                                   # follow redirects
```

## SQL basics

```sql
SELECT id, name FROM users WHERE age > 18 ORDER BY name LIMIT 10;
INSERT INTO users (name, age) VALUES ('a', 20);
UPDATE users SET age = 21 WHERE id = 1;
DELETE FROM users WHERE id = 1;
SELECT u.name, o.total FROM users u JOIN orders o ON o.user_id = u.id;
SELECT age, COUNT(*) FROM users GROUP BY age HAVING COUNT(*) > 1;
CREATE INDEX idx_users_email ON users(email);
```

| Join | Returns |
|---|---|
| INNER | Matches in both |
| LEFT | All left + matches |
| RIGHT | All right + matches |
| FULL | All from both |

## Auth terms

| Term | Meaning |
|---|---|
| Authentication | Who you are |
| Authorization | What you can do |
| Session | Server stores state, cookie holds id |
| JWT | Signed token: header.payload.signature |
| OAuth 2.0 | Delegated access (login with Google) |
| API key | Static secret per client |
| CORS | Browser rule for cross-origin requests |

## Common building blocks

| Block | Examples |
|---|---|
| Framework | FastAPI, Express, Spring Boot, Django |
| SQL DB | PostgreSQL, MySQL |
| NoSQL | MongoDB, DynamoDB |
| Cache | Redis |
| Queue | RabbitMQ, Kafka, SQS |
| Container | Docker |
