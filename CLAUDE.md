# CLAUDE.md — scholaops.ai Marketing Website

> Read this file in full at the start of every session before making any decisions or writing any code.

---

## 1. What this project is

The public marketing website for **scholaops.ai** — an AI-powered admissions platform for schools.

This is a **static marketing site only**. It has no backend, no auth, no shared code with the product repo (`school-sales-ai`). Its sole job is to explain the product, build trust with school administrators, and drive demo bookings.

**Live domain:** `scholaops.ai`
**Deployment:** Vercel (auto-deploy from `main`)
**Product repo (separate):** `school-sales-ai` — never import from it

---

## 2. The product this site sells

scholaops is an AI admissions platform for schools. Two core products:

**AI Widget**
- Embeddable chat widget for the school's website
- Powered by Claude (Anthropic) — the AI agent is named **Ada**
- Qualifies prospective families 24/7, answers questions from the school's own knowledge base
- Assigns a lead score per interaction
- When a prospect reaches a score threshold, surfaces a WhatsApp CTA

**CRM**
- Web admin panel for the admissions team
- Kanban pipeline: New → Qualifying → Warm → Hot → Closing → Enrolled → Discarded
- Lead list with scores, stages, and full conversation history (web + WhatsApp unified)
- Internal notes per lead
- Funnel reports

**The key differentiator — WhatsApp handoff:**
Web chat → WhatsApp transition with full context preserved. The prospect doesn't repeat themselves. The AI continues the conversation in WhatsApp. When a human from the school takes over, the AI pauses automatically (kill switch). This is the product's #1 competitive advantage, especially in LATAM where WhatsApp is the dominant communication channel.

**Long-term vision:**
scholaops is not just a CRM — it is an **AI hub for school operations**. Future modules beyond admissions include: internal FAQ agent, academic agent, administration agent, and more. The admissions widget is the entry point.

---

## 3. Target market

- **Now:** Small to mid-size private schools in Mexico (pilot: Instituto Via Diseño, Querétaro)
- **Soon:** LATAM private/independent schools broadly
- **Later:** Any school that needs AI-powered operations tooling (B2B SaaS, multi-tenant)

The buyer is a **school administrator or admissions director** — not a developer. Copy and UX should reflect that: warm, professional, results-focused. Not generic English SaaS jargon.

---

## 4. Tech stack — do not propose alternatives

| Layer | Technology |
|---|---|
| Framework | Astro (latest stable) |
| Styling | Tailwind CSS |
| Language | TypeScript |
| Package manager | pnpm |
| Deployment | Vercel |
| Domain | scholaops.ai |

- No React unless a specific interactive section requires a component island — use Astro's island architecture (`client:load` / `client:visible`) sparingly
- No CSS modules, no inline `style` props — Tailwind classes only
- No i18n library needed — single language (Spanish) for now. Astro's built-in i18n routing (`/es/`, `/en/`) can be added later when expanding to English without a painful migration.

---

## 5. Language and copy

- **All copy is in Spanish (Mexico).** Warm, professional tone — not stiff corporate Spanish, not casual.
- Brand names, product names, and technical terms stay in English: `scholaops.ai`, `Ada`, `CRM`, `widget`, `WhatsApp`, `Seed / Grow / Network` tier names.
- Prices are in **MXN**.

---

## 6. Design system

Based on the Claude Design prototype (`scholaops.ai Landing.html`). Reproduce faithfully.

**Palette:**
```
--cream:    #F2EFE6   (page background)
--cream-2:  #ECE8DA
--paper:    #FAF8F2
--ink:      #0E0D0A   (primary text)
--ink-mute: #6B6660   (secondary text)
--ink-line: #D9D3C2   (borders)
--lime:     #D7F26B   (accent / CTA highlight)
--lime-dk:  #B7D640
--moss:     #2A3826
--coral:    #F37056
```

**Typography:**
- Display / headings: `Instrument Serif` (italic for emphasis words)
- UI / body: `Space Grotesk`
- Labels / mono details: `JetBrains Mono`

**Design language:** warm cream base, electric lime as the AI signal color, dark ink sections for product deep-dives, floating animated cards for product visualization.

---

## 7. Site structure

```
/                   Landing page (single page, all sections)
```

Single-page for now. Sections in order:
1. Nav (floating pill, fixed)
2. Hero — headline + Ada phone mockup + floating score/pipeline cards
3. Marquee — "Pilotando con" → Via Diseño (only real client, no fake schools)
4. Products overview — Widget + CRM side by side
5. Widget deep dive (dark section)
6. CRM deep dive (dark section)
7. How it works — 3 steps
8. Stats — only use real data; remove or replace with honest copy until pilot data exists
9. Pricing
10. Final CTA
11. Footer

---

## 8. Pricing

Priced per campus, not per seat. In MXN. Annual billing.

| Tier | Price | Target |
|---|---|---|
| Seed | $7,900 MXN/mo | One campus, up to 5 users, up to 1,000 leads/mo |
| Grow | $17,900 MXN/mo | Growing schools, unlimited users & leads, WhatsApp channel |
| Network | Custom | School networks, multi-campus |

These are working numbers — validate after pilot.

---

## 9. CTAs and conversion model

**No free trials.** The product requires hands-on onboarding and the pilot phase needs high-touch relationships. Every CTA drives a demo booking.

- Primary CTA: **"Agendar demo"**
- Supporting CTA: **"Ver en 90 segundos"** (scrolls to product video/demo section)
- Final CTA section copy: *"Agendamos una demo de 20 minutos y lo dejamos funcionando en tu sitio ese mismo día."*

Demo bookings go to Calendly (embed or redirect — link TBD).

---

## 10. What NOT to put on this site

- Fake social proof (invented school names, fabricated stats) — only use real data
- "14-day free trial" or "No credit card required" — not the model
- Feature claims that aren't built: email open tracking, 11-language auto-detection, brochure sending, ML-trained lead scoring
- Anything about multi-tenant / SaaS network features until they exist

---

## 11. Project conventions

- Named exports only — no default exports
- `async/await` only — no `.then()/.catch()` chains
- Astro components in `src/components/`, pages in `src/pages/`
- No barrel `index.ts` files
- Component filenames: `PascalCase.astro`
- No comments that explain what the code does — only comment non-obvious WHY
