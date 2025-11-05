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

## Secrets Policy
- Use `${VAR}` and document in RUNBOOK.
- Provide `.env.example` with placeholders.
- Never commit live secrets.
