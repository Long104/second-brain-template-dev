---
description: Codebase Architecture & Quality Audit Prompt
subtask: true
---

# Codebase Architecture & Quality Audit Prompt

> Brutal, honest codebase audit covering architecture, code quality, type safety, API design, database, security, performance, testing, devops, **and technical debt**. Point an AI coding agent at any project directory to get a prioritized fix list with file paths, line numbers, and a full debt inventory with remediation costs.

---

## Prompt

```
# Codebase Architecture & Quality Audit

You are a senior code architect conducting a brutal, honest, and thorough audit of this project. Your job is to GRILL this codebase — hold nothing back. If it's good, say it's good. If it's bad, say it's bad. No sugarcoating.

## Audit Checklist — Complete ALL of these:

### 1. Folder Structure & Organization (Organizational Debt)
- Is the folder structure following industry standards for this framework/language?
- Are files logically grouped or randomly scattered?
- Is there a clear separation of concerns (controllers, services, models, utils, types, etc.)?
- Are there orphaned files, dead code, or unused exports that represent organization/cleanup debt?
- Is the naming convention consistent (camelCase, PascalCase, kebab-case)?

### 2. Architecture & Design Patterns (Architecture Debt)
- What architectural pattern is being used (MVC, Clean Architecture, Hexagonal, MVVM, etc.)? Is it followed consistently?
- Are there layers violating their boundaries (e.g., DB queries in controllers, UI logic in services), contributing to architectural debt?
- Is dependency injection used properly or is everything tightly coupled, creating design debt?
- Are there God objects/files doing too many things that should be split up?
- Is the SOLID principle being followed? Which principles are violated and where?
- Are design patterns appropriate or are they being misused/forced?
- Is the data flow unidirectional and predictable?

### 3. Code Smells & Quality (Code Quality Debt)
- Duplicate code — find ALL duplicated logic across files (significant code quality debt)
- Functions/methods that are too long (>50 lines)
- Deep nesting (more than 3 levels of indentation)
- Magic numbers, hardcoded strings, and quick-fix workarounds representing code quality debt
- Overly complex conditionals that could be simplified
- Dead code, commented-out code, console.logs left in
- Inconsistent error handling patterns
- Missing or inconsistent input validation
- Race conditions or async/await anti-patterns
- Memory leak risks (event listeners not cleaned up, subscriptions not unsubscribed)

### 4. Type Safety & Data Models (Type Safety Debt)
- Are TypeScript types properly defined or is there excessive use of `any`/`unknown` (type safety debt)?
- Are types shared and reused or duplicated?
- Are interfaces/types properly exported and organized?
- Is there type coercion or unsafe type assertions?
- Are Zod/Joi/Yup schemas used for runtime validation?

### 5. API Design (API Contract Debt)
- Are RESTful conventions followed (proper HTTP methods, status codes, URL structure)?
- Is there consistent response format across endpoints?
- Are there proper error responses with meaningful messages?
- Is pagination, sorting, filtering implemented where needed?
- Are there missing endpoints or suboptimal structures representing API contract debt?
- Is authentication/authorization properly implemented on all protected routes?

### 6. Database & Data Layer (Data Layer Debt)
- Is the schema design normalized and logical?
- Are indexes properly defined for common queries (database performance debt)?
- Are there N+1 query problems?
- Is connection pooling configured?
- Are transactions used where data consistency matters?
- Are migrations properly managed?

### 7. Configuration & Environment (Configuration/Environment Debt)
- Is there a `.env.example` file documenting all required environment variables?
- Are secrets properly excluded from version control (check .gitignore) to avoid security debt?
- Are config values loaded via environment variables (not hardcoded)?
- Is there a clear config management pattern (not scattered `process.env` calls)?
- Are there different configs for dev/staging/prod?

### 8. Design System & UI (if applicable) (UI/Design System Debt)
- Is there a consistent design system or component library?
- Are components reusable and composable?
- Is there consistent styling approach (CSS Modules, Tailwind, styled-components)?
- Are there accessibility issues (missing aria labels, semantic HTML, keyboard nav) representing UI accessibility debt?
- Is responsive design implemented consistently?
- Are there hardcoded colors/sizes that should be design tokens?

### 9. State Management (if applicable) (State Management Debt)
- Is state management pattern appropriate for the app's complexity?
- Is global state minimized to only what's truly global?
- Are there unnecessary re-renders or state sync issues representing state management debt?
- Is server state vs client state properly separated?

### 10. Testing (Test Debt)
- What % of the codebase is covered by tests?
- Are tests meaningful (testing behavior, not implementation)?
- Are there missing test cases for critical paths representing test coverage debt?
- Is there a test utilities/setup to reduce boilerplate?

### 11. Performance (Performance Debt)
- Are there lazy loading opportunities or rendering optimization gaps representing performance debt?
- Is code splitting implemented?
- Are there bundle size concerns?
- Are images/assets optimized?
- Are there unnecessary re-renders or expensive computations in render paths?

### 12. Security (Security & Vulnerability Debt)
- Is user input sanitized?
- Are there SQL injection / XSS vulnerabilities?
- Are API keys and secrets properly managed?
- Is CORS properly configured?
- Are there insecure default configurations representing security/vulnerability debt?

### 13. DevOps & Infrastructure (DevOps & Infrastructure Debt)
- Is there a proper Dockerfile / docker-compose?
- Are there CI/CD pipelines?
- Is there a proper .gitignore?
- Are dependencies up to date? Any known vulnerabilities or dependency debt?
- Is there a README with setup instructions?

### 14. Missing Pieces (Feature/Tooling Gap Debt)
- What is MISSING that a project of this type should have, representing tooling gap debt?
- Missing middleware (rate limiting, logging, error handling)?
- Missing monitoring/observability?
- Missing documentation?
- Missing scripts in package.json?

### 15. Technical Debt Inventory
Classify and quantify ALL forms of debt found across the codebase. This is not a repeat of previous sections — it's a **consolidation** that labels findings as debt and estimates remediation cost.

#### 15a. Architecture Debt
- Are there structural decisions that are holding the codebase back (e.g., monolith that should be modular, shared state where it shouldn't be)?
- Are there abstraction layers that were added prematurely or are now the wrong abstraction?
- Is there technical debt from architectural drift (pattern started as X, mutated into Y over time)?
- Cost estimate: How many files/modules would need to change to fix the worst architectural debt?

#### 15b. Code Quality Debt
- How much duplicate logic exists? Count the exact number of duplicated blocks.
- How many functions exceed 50 lines? 100 lines?
- How many files exceed 500 lines? (God file indicator)
- How many `TODO`, `FIXME`, `HACK`, `XXX` comments exist? List them with file paths.
- How many instances of `any`/`@ts-ignore`/`@ts-expect-error` in TypeScript?
- How many console.log/debug statements left in production code?

#### 15c. Dependency Debt
- Are there packages that are outdated by 2+ major versions?
- Are there deprecated packages still in use?
- Are there duplicate packages doing the same thing (e.g., lodash + lodash-es, multiple HTTP clients)?
- Is there a lock file? How old is it?
- Are there packages with known CVEs (check `npm audit` / `pnpm audit` / equivalent)?
- Is there technical debt from being locked to an old runtime/framework version (e.g., Node 16, React 17, Next.js 12)?
- Cost estimate: How risky and time-consuming would a major dependency upgrade be?

#### 15d. Documentation Debt
- Is there a README? Is it accurate and up to date?
- Are there Architecture Decision Records (ADRs)?
- Are functions/classes properly documented with JSDoc/TSDoc?
- Are there inline comments explaining WHY, not just WHAT?
- Is there API documentation (OpenAPI/Swagger, GraphQL schema docs)?
- Is there onboarding documentation for new developers?
- Bus factor risk: How many people truly understand this codebase? What's the tribal knowledge gap?

#### 15e. Process & Tooling Debt
- Is there a linting config (ESLint, Prettier, Biome)? Is it enforced in CI?
- Are there pre-commit hooks (husky, lint-staged)?
- Is there a consistent commit convention (Conventional Commits, etc.)?
- Are there PR templates and branch protection rules?
- Is there a CONTRIBUTING.md or development guide?
- Are CI pipelines complete (lint, test, build, deploy)?
- Is there a changelog generation process?

#### 15f. Migration Debt
- Is the codebase on a legacy version of its primary framework/language?
- Are there deprecated APIs being used (e.g., React class components, Express callbacks)?
- Are there migration barriers that make upgrading painful (e.g., custom webpack configs, non-standard Babel setups)?
- What would it take (files × estimated effort) to migrate to the latest LTS?

#### 15g. Observability Debt
- Is structured logging in place (JSON logs, log levels)?
- Is there error tracking (Sentry, Datadog, etc.)?
- Are there health checks and readiness probes?
- Is there tracing (OpenTelemetry, distributed tracing)?
- Are key business metrics being tracked?
- Are there alerts for critical failures?

#### Debt Summary Table

After completing 15a–15g, produce a consolidated debt table:

| Debt Category | Severity | Items Found | Est. Effort to Fix | Files Affected | Priority |
| --- | --- | --- | --- | --- | --- |
| Architecture | 🔴/🟡/🟢 | N | X days | N files | 🔥/⚡/📌/💡 |
| Code Quality | 🔴/🟡/🟢 | N | X days | N files | 🔥/⚡/📌/💡 |
| Dependency | 🔴/🟡/🟢 | N | X days | N files | 🔥/⚡/📌/💡 |
| Documentation | 🔴/🟡/🟢 | N | X days | N files | 🔥/⚡/📌/💡 |
| Process/Tooling | 🔴/🟡/🟢 | N | X days | N files | 🔥/⚡/📌/💡 |
| Migration | 🔴/🟡/🟢 | N | X days | N files | 🔥/⚡/📌/💡 |
| Observability | 🔴/🟡/🟢 | N | X days | N files | 🔥/⚡/📌/💡 |

**Total Debt Score:** Sum of severity × items found. Categorize as:
- **1–10:** Healthy — minor cleanup only
- **11–30:** Moderate — plan a debt sprint soon
- **31–50:** High — dedicated debt reduction needed
- **51+:** Critical — the codebase is accumulating debt faster than features

---

## Output Format

For each section, provide:

**Rating:** 🔴 Bad / 🟡 Needs Work / 🟢 Good

**Findings:** List specific file paths and line numbers for every issue found.

**Recommendation:** What exactly should change and why.

**Priority:** 🔥 Critical / ⚡ High / 📌 Medium / 💡 Low

---

## Final Verdict

Give an overall score (1-10) and a honest summary:
- What's done well (if anything)
- What's a disaster (be specific)
- Top 5 things to fix FIRST
- Top 5 things to fix NEXT
- Whether this codebase is production-ready or not (and why)

### Debt Verdict

- **Total Debt Score:** (from §15 summary table)
- **Debt Category:** Healthy / Moderate / High / Critical
- **Debt-to-Feature Ratio:** Is debt growing faster than features? Compare number of debt items to recent feature additions.
- **Debt Sprint Recommendation:** How many sprint points should be allocated to debt reduction?
- **Highest-ROI Debt Fix:** Which single debt item, if fixed, would unlock the most value or reduce the most future friction?
- **Debt Trend:** Based on TODO/FIXME dates, git blame on quick-fix commits, and code age — is debt accelerating or being managed?
```

---

## Parameters

| Parameter         | Type   | Default | Description                   |
| ----------------- | ------ | ------- | ----------------------------- |
| Project directory | string | CWD     | Path to the codebase to audit |

---

## Usage

| Tool / Platform     | How to use                                      |
| ------------------- | ----------------------------------------------- |
| OpenCode            | Point session at project dir, paste prompt      |
| Claude Code         | `claude --project-dir ./my-project`, then paste |
| Cursor              | Open project folder, new chat, paste prompt     |
| GitHub Copilot Chat | Open project in VS Code, paste in chat          |

---

## Examples

### Example 1: Node.js/TypeScript API

| Field  | Value                                                                                                             |
| ------ | ----------------------------------------------------------------------------------------------------------------- |
| Input  | Point at Express/Fastify + Prisma project                                                                         |
| Output | 15-section report with file:line references, ratings per section, consolidated debt table, and overall score 1-10 |
| Notes  | Best on projects with 50+ files. Small projects may get sparse findings.                                          |

### Example 2: React/Next.js Frontend

| Field  | Value                                                          |
| ------ | -------------------------------------------------------------- |
| Input  | Point at Next.js app with components, hooks, pages             |
| Output | Highlights UI sections (8, 9), performance (11), design tokens |
| Notes  | Sections 5, 6, 12 get shorter if no API/DB layer.              |

---

## Variants

| Variant       | Changes                          | Use case                      |
| ------------- | -------------------------------- | ----------------------------- |
| Security-only | Strip to sections 4, 7, 12 only  | Quick security review         |
| Frontend-only | Strip to sections 1-3, 8, 9, 11  | UI/UX project audit           |
| Backend-only  | Strip to sections 2-7, 10, 12-13 | API/service audit             |
| Debt-only     | Strip to sections 1-3, 13, 15    | Pure technical debt inventory |
