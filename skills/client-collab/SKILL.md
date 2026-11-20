---
name: client-collab
description: Use for any UI, website or app build where taste matters. Runs the build like a studio working with a client. Pauses at defined gates, shows visual options, asks for photos, references and assets, records decisions, and revises from feedback instead of guessing.
---

# Client Collab

Build what the client wants, not what the model thinks looks best. Taste belongs to the client. Every unknown that affects the look is decided by the client at a gate, with something to look at.

## 0. Modes
- collab (default for UI work): run the gates below.
- autopilot: only when the user's message contains the literal word "autopilot". Make choices from the brief, record them in DECISIONS.md as assumed, and run only Gate 6.
- The user can switch at any time ("autopilot from here", "ask me again at typography").

## 1. How to pause (works in any tool)
- Ask in chat, then END YOUR TURN. Do not build, edit or run anything until the user replies. If the tool has a question widget, use it.
- At most 3 questions per gate (Gate 0 may ask up to 4). Use plain language about looks and content, never jargon.
- Choice gates (1, 2, 3): give 2 to 4 labeled options and an "other / you decide" option. You may mark one option "(recommended)", but never the option that the product name, category or your first idea suggests, and say in one line why you recommend it.
- Approval gates (4, 5, 6): never mark any option as recommended and never put "approve" first. Options are: "Change something (say what)", "Looks right", "Not close, redo". Ask "what would you change?" before "do you approve?".
- Every gate message ends with a HOW TO VIEW block: the exact command to start a static server on port 8099 (python3 -m http.server 8099), the full URL of each preview or page (http://localhost:8099/...), and the paths of any saved screenshots. If the user cannot see the thing, do not ask them to judge it.
  Delivery mode:
  1. Local mode: if the agent runs on the user's own machine, keep the current localhost:8099 instructions.
  2. Remote mode: if the agent runs in a cloud sandbox or chat (the user cannot open localhost), never give a localhost link. Deliver each preview as the tool's file/artifact delivery (HTML file or published artifact) and also attach screenshots from previews/shots/.
  3. If the environment is unknown, ask once: "Can you open http://localhost:8099 on your computer?" and record delivery: local or remote in DECISIONS.md.
  4. If screenshots cannot be taken (no Playwright), say so and send the HTML file; never claim the user "saw" a preview.
- Never re-ask anything already in DECISIONS.md. If the answer is "you decide", choose, record it as assumed, move on.
- Keep gate messages short: what you made, what you need, your recommendation.

## 2. DECISIONS.md (the project's memory)
Create it at the start. Sections: Brief summary / Assets (path and status: received, missing, placeholder) / References (link or file, and what to take from it) / Direction (archetype, style, palette, type, motion personality, 3D plan) / Taste dials from 1 to 5 (boldness, density, darkness, playfulness, realism, motion intensity) / Approved / Rejected (with the reason) / Open items / Revision log (round, client comment, what changed). Every later skill reads this file first.

## 3. Gates
Gate 0, Intake. After reading the brief, collect assets and references using skills/asset-intake. Reference board (part of Gate 0). Ask for references by slot, because components, cursors and whole templates teach different things. Tell the user they may paste links, or drop screenshots or screen recordings into a references/ folder, and may skip any slot:
1. Whole site or template: overall layout, pacing, feel.
2. Components: cards, buttons, navigation, forms, footers.
3. Cursor effects.
4. Text animation: headlines, paragraphs, kinetic type.
5. Backgrounds and 3D environments.
6. Scroll behavior and page transitions.
Examples of places people collect from: 21st.dev, React Bits, OriginKit, ThreeUI, Cult UI, Codrops, Awwwards. Write REFERENCES.md with one row per item: slot, link or file, what to take, where it will be used. If a link cannot be opened, ask for a screenshot or screen recording; never guess a reference from its URL. Follow reference-teardown for each item. Take mechanics and structure; copy code only when the item's license allows it, with attribution recorded in assets/README.md. At the start of Gate 1, show the REFERENCES.md table in chat and ask the user to correct it. Where a slot is empty, say which default you will propose, and let the user add references at any later gate. Missing assets get a stated placeholder plan, never silent invention. For physical products (perfume, shoes, devices) ask for photos before designing the hero.
Gate 1, Direction. Build previews/direction.html with three genuinely different directions as cards: name, archetype, style, palette swatches, a sample using the real headline, a one-line signature moment. Ask: pick one, mix (say which parts), or give a new reference. Names are not palette briefs. A brand or product name (Noir, Sunrise, Ember, Forest) suggests a color; that is the first idea and is never the default. Gates 1 and 2 always offer three palettes, labeled: Literal (what the name suggests), Opposite (a contrasting mode or hue family), and Unexpected (derived from the product's real materials or setting). At least one of the three must have a light or mid-tone background unless the user asked for dark. Never mark the Literal one as recommended. At Gate 1 also ask the darkness dial in one line (1 light to 5 dark).
Gate 2, Type and color. Build previews/type-color.html with three type pairings on the chosen palette, rendered with the real headline, subheading, body, button and label. Ask: pick, adjust (more serious or playful, tighter or looser), and any palette tweak.
Gate 3, Motion and story. Build previews/motion.html with three live motion personalities (for example calm and cinematic, snappy and sharp, playful and bouncy): hero text reveal, section reveal, button hover, one scroll-linked element, one transition. Before the storyboard is approved, generate previews/motion-kit.html showing 3 live options per category (text, card, button, environment, cursor from cursors.md) and ask the client to pick one per category. Record picks in DECISIONS.md under motion_kit:. Then show the STORYBOARD.md shot list as a plain table. Ask: personality, preferred transitions, and approve or edit the scenes, their order and the signature moment. Approval options stay: "Change something (say what)", "Looks right", "Not close, redo". No recommended option on the approval question.
Gate 4, Hero check. After the first working hero built from the client's assets (see asset-intake), capture a screenshot and a short frame strip, and state what is real and what is placeholder. Ask: what would you change? Options: Change something (shape, material, lighting, camera, scale or color), Looks right, Not close and redo. Build no further scenes until approved. Gate 4 must include previews/shots/ with three hero screenshots (front, three-quarter, close-up at 2x). If the client supplied product photos, also save previews/shots/compare.png with the photo on the left and a render at the same angle on the right, and list what differs. If no photo exists, say clearly that the object is a PLACEHOLDER and name the real asset that would replace it.
Gate 5, Section reviews. Build in passes of 2 to 3 scenes. After each pass show frames and ask for feedback per section. One revision round per pass unless the client asks for more.
Gate 6, Final. Run Motion QA and the rubric from visual-qa, summarize the decisions, list known limitations and how to run it, and ask for last changes. Offer a Wow Pass.

## 4. Preview rules
- Previews are small standalone HTML files in previews/, quick to open. Give the exact way to view them (python3 -m http.server and the URL, or open the file directly when it needs no modules).
- Use real content: the client's name, headline and colors. Never lorem ipsum.
- Options must differ in style and mood, not be three shades of one idea. Label them A, B, C.
- Take principles from references, never their logos, copy, illustrations or licensed images.

## 5. Feedback translation (turn taste words into changes)
- "more premium" or "luxury": fewer elements, more whitespace, slower motion with softer easing, tighter palette, serif display, bigger scale contrast, subtle light.
- "more fun" or "playful": rounder shapes, saturated accent, overshoot easing, bigger hover reactions, friendlier copy.
- "more modern" or "techy": mono labels, grid lines, sharper corners, faster cuts, HUD details.
- "too busy": remove one effect per section, increase spacing, reduce simultaneous motion, mute secondary colors.
- "boring" or "too plain": add a depth layer (ghost wordmark), one scroll-linked moment, stronger scale contrast, light and shadow, texture.
- "feels cheap": remove gradients and glows, fix spacing rhythm and alignment, upgrade type, use real imagery, slow down, reduce saturation.
- "laggy": remove the heaviest effect, lower resolution, re-measure frame times.
- "hard to read": separate text and object zones, raise contrast, enlarge text.
- "make it pop": raise hero-versus-background contrast, one accent color, rim light, larger object.
Apply the smallest change that satisfies the comment, say what changed in one line, log it in DECISIONS.md and adjust the taste dials. If the comment is vague, offer 2 or 3 concrete variants instead of guessing.

## 6. Revisions
- Make every revision a minimal diff (diff-guard).
- Show what changed, with before and after screenshots when possible.
- After 3 rounds on the same point, show 3 variants and let the client pick.

## 7. Rules
- Never silently invent brand facts, product details, prices, testimonials or claims. Label placeholders PLACEHOLDER.
- If photos or a model of the client's product exist, never substitute a generated shape for it. Use asset-intake.
- If the client is unavailable (autopilot), continue and flag every assumption.
- Every skill reads DECISIONS.md before acting.

## 8. Final check
- [ ] DECISIONS.md exists and matches what was built.
- [ ] Each gate was run or explicitly skipped by the user.
- [ ] No gate asked more than 3 questions (Gate 0: 4).
- [ ] Rejected options never reappeared.
- [ ] Every asset was supplied by the client or labeled placeholder.