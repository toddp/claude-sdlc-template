# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

NOTE: all file paths are relative to the project root.

> You are Claude Code. Read:
> - `/.llm/handbook/00-Working-With-Claude.md`
> - `/.llm/handbook/10-Architecture-Principles.md`
> - `/.llm/handbook/20-Quality-Standards.md`
> - `/.llm/handbook/30-Testing-Standards.md`
> - `/.llm/handbook/40-Security-&-Privacy.md`
> - `/.llm/handbook/50-DevEx-&-Tooling.md`
> - `/.llm/handbook/60-Docs-&-Decision-Log.md`
> - `/.llm/handbook/70-Prompting-&-Context.md`
> - `/project/PROJECT_BRIEF.md`
> - `/ARCHITECTURE.md` ← **Project-specific architecture details**
>
> Respond in this sequence:
> 1) **QUESTIONS** (max 5, only what blocks progress).
> 2) **SPEC** (use `/.llm/templates/SPEC.md`), citing handbook sections.
> 3) **ADR** proposal (use `/.llm/templates/ADR.md`).
> 4) **STOP — AWAIT APPROVAL** before proceeding to implementation.
> 5) **TASKS** with estimates and risks.
> 6) **CHANGE PLAN** (files to add/edit).
> 7) **CODE + TESTS**, ending with **RUN INSTRUCTIONS** and README/RUNBOOK updates.
> 8) **SELF-REVIEW** (use `/.llm/templates/SELF_REVIEW_CHECKLIST.md`) before declaring feature complete.
> 9) **BROWSER VERIFICATION** using Playwright to confirm UI features work as expected.
>
> **Autonomy Mode: ON** when I say so. Iterate until `scripts/quality_gate.sh` passes, self-review approved, Playwright browser tests confirm UX, and all Acceptance Criteria are met.


## Autonomy Mode Trigger

**"Autonomy Mode: ON"** can only be said by the user AFTER:
- SPEC has been reviewed and approved by the user
- ADR has been reviewed and approved by the user
- User explicitly grants permission to proceed with implementation

**I will NEVER assume Autonomy Mode is ON unless you explicitly say so.**

NOTE: For new projects, Autonomy Mode begins only *after* the IMPLEMENTATION_PLAN.md is approved.

## What NOT to Do

- **DO NOT** proceed past SPEC + ADR without explicit user approval
- **DO NOT** assume "yes use your recommendations" means "start coding"
- **DO NOT** batch multiple SDLC phases together without pausing for approval
- **DO NOT** enter Autonomy Mode unless user explicitly says "Autonomy Mode: ON"
- **DO NOT** skip the approval checkpoint after SPEC + ADR

## Browser Verification with Playwright

For any feature with UI changes, you MUST verify using Playwright:

```javascript
// Create test in test/playwright/feature_name_test.js
const { chromium } = require('playwright');

// Test the actual user flow
// Capture screenshots for confirmation
// Verify acceptance criteria are met in the browser
```

Run verification: `node test/playwright/feature_name_test.js`

Features are NOT complete until browser verification passes.

---

## Project-Specific Information

**See `/ARCHITECTURE.md` for:**
- Technology stack details
- Development commands
- Multi-tenancy or auth patterns
- External service integrations
- Code style guidelines specific to this project
- Database schema overview
- Deployment configuration

**Important:** Always read ARCHITECTURE.md at the start of a conversation to understand this project's specific architecture and conventions.
