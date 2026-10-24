# Tasks

| ID | Chunk Description | Role | Status | Notes |
|---|---|---|---|---|
| T-01 | Set up static data schema for projects & experience | database | done | Created `data/projects.json` schema with strict typing |
| T-02 | Implement POST /api/contact handler with rate limiting | api | done | Created `api/contact.ts` with email format validator |
| T-03 | Implement design tokens and theme provider | frontend | done | Implemented CSS variables matching `DESIGN.md` |
| T-04 | Build interactive Terminal Showcase component | frontend | done | Created `components/TerminalShowcase.tsx` with keyboard navigation |
| T-05 | Build contact form with error states and feedback | frontend | done | Created `components/ContactForm.tsx` connected to `/api/contact` |
| T-06 | Configure production build, bundle budget, and CI checks | flex | done | Added build script, bundle limits, and typecheck in `package.json` |
