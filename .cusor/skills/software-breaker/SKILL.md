---
name: software-breaker
description: >-
  Pushes software to its limits to find bugs, edge-case failures, weak spots,
  and missing tests; proposes concrete improvements. Full Chaos mode by default.
  Use when the user asks to teste à fond, casse ça, chaos test, trouve les bugs,
  /software-breaker, revue pré-release, pre-release review, break it, find bugs,
  stress test, or wants aggressive QA before release.
---

# Software Breaker

Full Chaos testing agent. Treat the system as an adversary: stress it, break assumptions, prove failures with reproduction steps, then propose fixes and missing tests.

## Guardrails

- No malware, exploits against third-party systems, or credential theft
- No dumping secrets, tokens, or `.env` contents in reports
- Every finding must be reproducible (steps + expected vs actual)
- Do not patch code unless the user explicitly asks
- Stay defensive on security: report vulnerabilities, do not weaponize them

## When to use

| Situation | Action |
|-----------|--------|
| User triggers listed in description | Read this skill, launch `software-breaker` subagent |
| Narrow scope (single file/function) | Subagent or inline, apply attack matrix to scope only |
| Pre-release / full app | Subagent with full repo scope + runtime when env allows |
| User asks to fix findings | Switch to implementation mode after report |

## Launch subagent

Launch exactly one `software-breaker` subagent via Task tool:

- `subagent_type`: use `generalPurpose` with the software-breaker agent file, or invoke by name if available
- `description`: `"Software Breaker"`
- `run_in_background`: `false` unless user asks for background

Prompt shape:

```text
Full Repository Path: <absolute repository path>
Target: <module, feature, diff, or "full pre-release">
Scope: <branch changes | uncommitted changes | full codebase | specific paths>
Custom Instructions: <only if user gave specific focus>
Report Language: <fr | en | match user language>
```

Default `Scope` to `branch changes` when reviewing recent work; use `full codebase` for pre-release.

If the subagent fails, retry once with `Scope: specific paths` and list the paths explicitly.

## Full Chaos workflow

Copy and track progress:

```
Software Breaker Progress:
- [ ] 1. Scope — define target and boundaries
- [ ] 2. Map — list attack surfaces (routes, jobs, UI, shared state)
- [ ] 3. Attack — run attack matrix by risk priority
- [ ] 4. Prove — reproduce each finding (tests, curl, UI, logs)
- [ ] 5. Report — bilingual severity table + improvements
- [ ] 6. Improve — missing tests + next attacks
```

### Step 1 — Scope

Clarify: what module/feature/diff? What is in bounds (local only vs staging)? What env is available (tests, API, browser)?

### Step 2 — Map surfaces

Identify entry points:
- HTTP routes / GraphQL / WebSockets
- CLI commands / background jobs / cron
- UI flows and form submissions
- Database writes and migrations
- External integrations (webhooks, Docker, third-party APIs)
- Shared mutable state (cache, sessions, files)

### Step 3 — Attack matrix

Apply [reference.md](reference.md) categories in risk order. For each surface, ask: *what happens at boundaries, under load, twice, with bad input, with no auth, with wrong auth?*

### Step 4 — Prove

- Run existing test suite; note gaps and failures
- Add or describe minimal repro cases (do not commit unless asked)
- Hit APIs with edge payloads when server is reachable
- Walk UI error paths when frontend is available
- Check logs and panics after chaos attempts

### Step 5 — Report

Use the report template below. Write in the user's language (FR or EN). Keep severity labels bilingual.

### Step 6 — Improve

For each finding, propose: concrete fix hint, test to add, monitoring/validation to add. Sort improvements by impact vs effort.

## Severity (bilingual)

| Label | When |
|-------|------|
| Critical / Critique | Data loss, auth bypass, RCE, payment/security breach, production down |
| High / Élevé | Wrong data, privilege escalation, crash loop, major feature broken |
| Medium / Moyen | Incorrect behavior under edge cases, poor error handling, flaky paths |
| Low / Faible | Minor UX issues, cosmetic, unlikely edge case |
| Improvement / Amélioration | Not a bug; hardening, coverage, observability, maintainability |

## Report template

```markdown
# Rapport Software Breaker / Software Breaker Report

## Verdict
[1-2 sentences: overall risk and readiness]

## Findings (triés par sévérité / sorted by severity)

| Sévérité / Severity | Zone | Bug / faille / Finding | Preuve / repro / Proof | Impact |
|---------------------|------|------------------------|-------------------------|--------|

## Améliorations / Improvements

1. [Priority] Concrete action
2. ...

## Couverture / trous de tests / Test coverage gaps

- Missing: ...
- To add: ...

## Prochaines attaques suggérées / Suggested next attacks

- ...
```

Each finding row must include enough repro detail to verify without guessing.

## Inline mode (no subagent)

When scope is tiny or subagent unavailable:

1. Read changed files and related tests
2. Apply attack matrix from [reference.md](reference.md)
3. Run relevant tests
4. Output report using template above

## Additional resources

- Attack matrices and checklists: [reference.md](reference.md)
- Installation and sharing: [INSTALL.md](INSTALL.md)
