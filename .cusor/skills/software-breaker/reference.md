# Software Breaker — Attack Reference

Concise matrices for Full Chaos testing. Apply in risk order; skip categories that do not apply to the stack.

## 1. Auth / sessions / JWT

- Missing or weak auth on protected routes
- Token expiry not enforced; refresh token reuse
- Algorithm confusion / none algorithm / weak secrets in dev leaking to prod patterns
- User A accesses User B resources (IDOR, horizontal privilege escalation)
- Logout does not invalidate session; stale tokens still work
- Generic vs specific error messages leaking account existence (when policy requires generic)
- Rate limiting absent on login/register/reset

**Probe:** no header, expired token, malformed token, wrong user ID in path/body, concurrent sessions

## 2. Validation and injection

- Missing validation on body, query, path, headers
- Type coercion surprises (string `"0"` vs int `0`, empty string vs null)
- Oversized payloads, deeply nested JSON, unicode/special chars
- SQL injection, command injection, path traversal in file ops
- XSS in rendered output (stored/reflected)
- SSRF in URL-fetching features

**Probe:** empty, null, max length+1, negative numbers, `%00`, `../`, `<script>`, SQL fragments, prototype pollution keys

## 3. Concurrency / races / idempotency

- Double submit creates duplicate records/charges/containers
- TOCTOU between check and act
- Goroutine/thread leaks; unbounded parallel provisioning
- Non-atomic read-modify-write on shared counters or status fields
- Retry logic causes duplicate side effects

**Probe:** parallel identical POSTs, interrupt mid-flow, retry same idempotency key with different body

## 4. Resource limits / timeouts / retries

- No timeouts on external calls (Docker, DB, HTTP)
- Memory/CPU limits not enforced under load
- Unbounded queues or goroutines
- Retry without backoff hammers failing dependency
- Disk full / quota exceeded behavior undefined

**Probe:** slow dependency simulation, large file upload, many concurrent requests, kill container mid-provision

## 5. API contract and error paths

- Wrong HTTP status codes (500 instead of 400/404/409)
- Success body on partial failure
- Inconsistent error shape; stack traces exposed to client
- Missing pagination limits; unbounded list endpoints
- Breaking changes without versioning

**Probe:** invalid JSON, wrong Content-Type, missing required fields, duplicate unique keys, delete nonexistent resource

## 6. UI / UX failure paths

- Forms submit with invalid state; no client validation feedback
- Loading/error/empty states missing or misleading
- Race: double click submits twice
- Token expiry mid-session: silent failure vs redirect
- Accessibility: keyboard trap, no focus on error

**Probe:** offline mode, slow network, back button after submit, refresh during async action

## 7. Data integrity and multi-tenant isolation

- Orphan records after failed transactions
- Cascade delete too aggressive or missing
- Tenant A data visible in Tenant B UI/API
- Clock skew affecting expiry, ordering, TTL
- Migration not reversible; partial migration state

**Probe:** create then force-fail second step, list resources as wrong tenant, timezone boundaries

## 8. Pre-release checklist

```
Pre-release Software Breaker:
- [ ] All Critical/High findings resolved or accepted with ticket
- [ ] Test suite green; new tests for each fixed bug
- [ ] Auth boundaries verified on every new route
- [ ] Env secrets not committed; prod config reviewed
- [ ] Error messages user-safe; logs detailed server-side
- [ ] Rate limits on public endpoints
- [ ] Rollback path documented for migrations/deploy
- [ ] Smoke test on staging: happy path + one chaos path per major feature
```

## Stack hints (detect from repo)

| Stack signal | Extra probes |
|--------------|--------------|
| Go + Fiber | panic recovery, middleware order, context cancellation |
| JWT | exp/iat/nbf, secret rotation, Bearer parsing |
| PostgreSQL | unique constraints, transaction boundaries, connection pool exhaustion |
| Redis | key TTL, cache stampede, wrong key namespace |
| Docker provisioning | partial create, label conflicts, network attach failures |
| Next.js | SSR/hydration mismatch, exposed env vars, client-side token storage |

## Finding quality bar

A valid finding includes:

1. **Location** — file:line or endpoint:method
2. **Steps** — numbered repro
3. **Expected** vs **Actual**
4. **Impact** — who/what breaks
5. **Fix hint** — one concrete direction (not full implementation unless asked)
