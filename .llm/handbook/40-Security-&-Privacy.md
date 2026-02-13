# 40 — Security & Privacy

## Data Classification (customize)
- Public / Internal / Confidential / Sensitive

## Threat Model Checklist
- Authn/Authz, least privilege
- Input validation & sanitization
- Secrets via env/vault; rotate regularly
- No secrets/PII in logs; correlation IDs
- Rate limiting & abuse controls on external endpoints
- Dependency SCA; pin versions; monitor CVEs

## SQL Injection Prevention (CRITICAL)

**ALWAYS use parameterized queries. NEVER use string interpolation in SQL.**

- Use `?` placeholders or hash conditions in ActiveRecord: `where("col = ?", val)` or `where(col: val)`
- Use `sanitize_sql_array` for raw SQL with dynamic values
- Use `connection.quote` for individual values in raw SQL
- NEVER use `#{}` interpolation or `+` concatenation in SQL strings
- PostGIS WKT strings must also be quoted with `connection.quote`

### SQL Code Review Checklist

Before merging any PR with SQL:
- [ ] All raw SQL uses `sanitize_sql_array` or `connection.quote`
- [ ] No string interpolation (`#{}`) in SQL strings
- [ ] No string concatenation (`+`) in SQL strings
- [ ] ActiveRecord query methods use `?` placeholders or hash conditions

## Pre-Commit Security Scanning

Before committing code changes, run Brakeman on changed Ruby files to catch security issues early:

```bash
# Scan only changed files (fast, targeted)
bundle exec brakeman --only-files $(git diff --name-only --diff-filter=d HEAD | grep '\.rb$' | tr '\n' ',') --no-summary --quiet

# Full scan (use for final validation or when quality gate runs)
make secscan
```

- Address any **critical** or **high** severity findings before committing.
- Medium/low findings should be reviewed but do not block commits.
- If a finding is a false positive, document it inline with `# brakeman:disable` and a justification comment.

## Secrets Policy
- Use `${VAR}` and document in RUNBOOK.
- Provide `.env.example` with placeholders.
- Never commit live secrets.
