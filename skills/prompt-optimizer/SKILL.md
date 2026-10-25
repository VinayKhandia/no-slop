---
name: prompt-optimizer
description: Use first on every build request. Turns a rough idea into a complete engineering brief (BRIEF.md) that unlocks the model's full capability: product, flows, stack, data model, API, auth, security, design and 3D direction, acceptance criteria and verification. Expands where it prevents rework, compresses where it is noise.
---

# Prompt Optimizer (Brief Builder)

Goal: convert a rough request into a brief that a senior team could build from without asking questions. Rework is where tokens and quality are lost, so expand the decisions that prevent rework and cut filler.

## 0. Modes (pick silently)
- quick: a fix, a copy change, one function. Restate it in one sentence plus one acceptance check. No BRIEF.md.
- build (default): a new feature or app. Write BRIEF.md.
- full: a new product, or anything touching accounts, stored data, payments, third-party APIs or deployment. Write BRIEF.md with every section and a risk list.
If the user says "just do it", skip questions and flag assumptions instead.

## 1. Read before you write
- Inspect the repo first: package or requirements files, folder layout, README, env examples, existing conventions. Reuse the existing stack and style over inventing a new one.
- Note the user's stated skill level and preferred languages. If teach-mode is on, plan teaching hooks.

## 2. Classify the request (more than one may apply)
- Marketing or brand site, immersive 3D site, web app (CRUD or dashboard), full-stack app with accounts, API or service, data or ML pipeline, CLI or bot, mobile.
- Classification decides which skills run: UI and 3D work uses design-taste, motion-craft, scene-3d. Server work uses the backend, data, API, auth and security sections below and their skills if present.

## 3. Question policy
- Ask only blocking questions: at most 5, in one message, each with a recommended default. A question is blocking if the answer changes the architecture, spends money, handles personal data, is irreversible, or the request contradicts itself.
- Everything else becomes an assumption listed in BRIEF.md so the user can correct it.
- Unattended or headless: never block. Assume, flag, continue.

## 4. BRIEF.md (each section as long as it needs, no padding)
1. Goal and success: the outcome in a paragraph, who uses it, what done looks like, and acceptance criteria written as testable statements.
2. Scope: must, should, will not (non-goals).
3. Users and flows: each primary journey step by step, including error, empty, loading and unauthorized states.
4. Architecture: stack with reasons, folder structure, services and boundaries, environment variables, third-party services.
5. Data: entities, fields, types, relations, indexes, constraints, migrations, seed data. Choose the database and justify it.
6. API: endpoint table (method, path, auth, request, response, errors), validation, pagination, rate limits, one consistent error format. For external APIs: auth method, rate limits, retries with backoff, webhook signature verification, a mock for development.
7. Auth and access: sign-in method, session or token strategy, roles and permissions, a route protection map, logout and revocation.
8. Security and privacy: threats specific to this app, secret handling, input validation, CORS and CSRF, rate limiting, logging without personal data, dependency hygiene.
9. UX and design: for UI work, list the inputs design-taste needs (audience, mood words, brand, assets) and which archetype or style is likely. Do not invent the visual design here.
10. Quality plan: tests (unit, integration, end to end), what visual-qa captures, performance budgets (page weight, FPS, response time), accessibility.
11. Delivery: run instructions, scripts, environment setup, deployment target, README outline.
12. Risks and open questions, each with a default.
13. Teaching hooks: 3 to 5 concepts worth explaining if teach-mode is on.

## 5. Decision defaults (use unless the request or the repo says otherwise)
- Language: match the repo, then the user's stated languages. Python: FastAPI with Pydantic. JavaScript: Node with Express or Fastify, or Next.js route handlers. Java: Spring Boot. Go: net/http or chi.
- Database: SQLite for local development, PostgreSQL for production. Use an ORM or query builder (Prisma, Drizzle, SQLAlchemy, JPA) and always use migrations. Add an index for every foreign key and every frequent filter. Use a document store, cache or queue only when a concrete need is stated.
- Auth with Google: OAuth 2.0 / OpenID Connect with PKCE through a maintained library (Auth.js, Passport, Authlib, Spring Security). Verify the ID token issuer, audience and expiry. Store the provider's stable user id (sub), not only the email. Prefer a server-side session in an HttpOnly, Secure, SameSite cookie over tokens in localStorage. Add CSRF protection to state-changing routes. Keep roles in the database. Never write your own crypto or password hashing.
- Secrets: .env plus a committed .env.example, validate environment variables at startup, never commit real secrets.
- API: REST with a consistent error shape, an OpenAPI document, idempotency keys for payments and webhooks, signature verification for incoming webhooks.
- Frontend: immersive 3D sites use vanilla ES modules or Vite with three.js, GSAP and Lenis. Apps use React or Next.js. Do not add a framework without a reason.
- Versions: read the lockfile or the package docs at build time. Do not trust memory for library APIs.

## 6. Working agreement (copy this into BRIEF.md)
- Build vertical slices end to end, then widen.
- Run the code: start the app, call the endpoints, run the tests, take screenshots. Never report done on code that was not executed.
- Write tests for business logic, auth rules and data constraints before polishing the UI.
- Read documentation and source instead of guessing an API.
- If the same error blocks you twice, change approach and say why.
- Handle failure states everywhere: network, empty, unauthorized, validation.
- State what was not verified.

## 7. Token discipline
- Reference other skills by name instead of repeating their rules.
- Do not restate the user's request. No filler.
- Put long reference material in files and link to it.

## 8. What to show the user (short)
Mode, project type, a five-line summary of the brief, the assumptions list. Ask for corrections only if a blocking question remains, then hand BRIEF.md to the planner.

## 9. Final check
- [ ] Every requirement became a testable acceptance criterion.
- [ ] Apps with users or storage have data, API and auth sections.
- [ ] Assumptions, risks and open questions (with defaults) are listed.
- [ ] A stranger could build from this brief without asking anything.