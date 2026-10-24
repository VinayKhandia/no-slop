# Learning Log

### T-01: Structured Project Schema Definition

- **What we did**: Created a strongly typed JSON schema and validated fixtures for portfolio projects and technical competencies.
- **Why**: Decoupling raw data from presentation components allows instant content updates without touching React rendering logic.
- **Core concept**: Single source of truth. Keeping data pure prevents rendering bugs when schemas evolve.
- **Analogy**: Like writing the ingredients on recipe index cards rather than painting them onto the kitchen wall.
- **Try it yourself**: Add a new key `"wip": true` to `projects.json` and verify if your schema parser catches untyped additions.

---

### T-02: Rate-Limited Contact API Endpoint

- **What we did**: Implemented a POST route handler with input validation and in-memory IP token-bucket rate limiting.
- **Why**: Protects submission endpoints from automated spam bots and inbox flooding without requiring third-party captchas.
- **Core concept**: Rate limiting restricts the frequency of repeated requests within a sliding time window.
- **Analogy**: Like a turnstile at a subway station that only admits one passenger every few seconds.
- **Try it yourself**: Send five rapid `curl -X POST` requests to the endpoint in your terminal and observe the 429 status response.

---

### T-03: Design Token System Integration

- **What we did**: Converted colors, spacing units, and typography scales from `DESIGN.md` into CSS custom properties.
- **Why**: Centralizing design tokens enables seamless theme changes and ensures visual consistency across all components.
- **Core concept**: Indirection. Components reference semantic variable names rather than raw hardcoded hex codes.
- **Analogy**: Swapping paint colors by changing labels on the mixing palette rather than repainting every individual frame.
- **Try it yourself**: In devtools, change `--color-accent` from `#2EA043` to `#388BFD` to watch every active indicator shift color together.

---

### T-04: Terminal Showcase Component

- **What we did**: Built an interactive terminal window with arrow-key navigation and simulated command execution.
- **Why**: Gives visitors a memorable, interactive way to inspect projects while demonstrating frontend DOM manipulation skills.
- **Core concept**: Event-driven state machine. Keystrokes dispatch predictable state transitions to update history lines.
- **Analogy**: Like a vending machine: inserting a specific coin sequence dispenses the exact selected item reliably.
- **Try it yourself**: Press `Tab` inside the terminal component to see if focus management correctly traps keyboard navigation.

---

### T-05: Resilient Contact Form

- **What we did**: Connected the contact form to `/api/contact` with optimistic UI states and detailed error handling.
- **Why**: Clear error feedback prevents users from abandoning forms when network drops or validation fails.
- **Core concept**: State reconciliation between asynchronous network calls and immediate UI presentation.
- **Analogy**: Like receiving a postal tracking number immediately when handing a package over the counter.
- **Try it yourself**: Disconnect your internet connection and click submit to verify whether the offline banner renders gracefully.

---

### T-06: Production Bundle Budgeting

- **What we did**: Added size-limit verification and strict compiler checks to the project build script.
- **Why**: Prevents accidental introduction of heavy dependencies that degrade First Contentful Paint.
- **Core concept**: Performance budgets. Setting hard byte ceilings guarantees software stays fast as features accumulate.
- **Analogy**: Setting a maximum weight limit on airline luggage before boarding.
- **Try it yourself**: Run `npm run build` and inspect the output terminal table showing individual chunk sizes in kilobytes.
