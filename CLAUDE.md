# CLAUDE.md

This file provides product and team context for AI-assisted hypothesis discovery work. It is not a code project — it is a product strategy document. Read it to understand who the user is, what they've already validated, and what they're trying to figure out next.

---

## Product context

**Product:** AI Augmentation Platform for bank IT teams
**What it does:** Identifies high-friction roles inside banks and ships AI tools that reduce manual time waste in those roles — without replacing people, augmenting their output.
**Stage:** Post-MVP on two shipped products; entering next hypothesis discovery cycle.
**Domain:** Russian/CIS bank IT departments — QA, analytics, business analysis, chatbot/IVR teams.

### Who I am

Product builder doing AI transformation inside banks. I find roles with measurable time waste, validate the pain, and ship lightweight AI tools (chatbots, agents, multiagent pipelines). Current focus: discovering the next role to augment after two proven cases.

**My technical profile:** Low-code / prompt engineering. I design solutions, write prompts, and configure tools — I don't write production code. Developers handle implementation.
**Tenure:** Less than a year embedded — still building trust. Interview access to new teams is not free; requires relationship effort or a warm intro.

### Target customer

**Role:** Team leads and heads of IT sub-departments inside the bank (support ops, analytics, chatbot/IVR teams).
**Context:** Teams of 5–30 people, sprint-based delivery, clear velocity metrics. Decision to try a tool is made at team lead level; budget approval goes to department head.
**Pain pattern:** Repetitive, rule-based, or lookup-heavy subtasks that consume 15–30% of sprint capacity — tasks the role considers "not real work" but has no time to automate.

### Engagement model

- **Internal team** — embedded inside one bank, not an external vendor
- **Funding:** Internal IT budget / cost center — no sales cycle, no external pricing
- **Access:** <1 year tenure — access to new teams requires trust-building; not all interview slots are easy to get
- **Team:** Product owner (me, prompt/low-code) + 1–2 developers (dedicated full-time)
- **AI stack:** Dual — external APIs (OpenAI / Anthropic) for prototyping; self-hosted open-source LLM (LLaMA / Mistral family) for production. Quality gap is real and significant. Always validate the hypothesis on the internal model before committing — structured tasks (RegExp, SQL) degrade less than reasoning-heavy or long-context tasks.

### How hypotheses are discovered

1. Market research — track how AI tools are changing specific role workflows externally (e.g. new tooling releases, role-specific AI adoption)
2. Interviews — go to the team, map their workflow, find where time is actually spent

### Hard constraints

- **No sensitive personal data** — don't build on PII, transaction data, or credit history
- **Augment, don't replace** — tools must make existing people more productive; headcount-reduction framing is off the table (see DL-2 for why this also fails technically)

---

## Shipped products (already validated, not hypotheses)

### DL-0 — RegExp Auto-Generator for chatbot scenario writers
- **Who:** Scenario writers building NLU training data for bank chatbots/IVR
- **Pain:** Writing RegExp patterns for intent matching consumed ~30% of sprint time
- **Solution:** LLM-assisted RegExp generation from natural language intent description
- **Result:** 30% sprint time recovered for scenario writers
- **Status:** Shipped ✓

### DL-1 — Text→SQL multiagent system for data analysts
- **Who:** Bank data analysts running ad-hoc queries for business stakeholders
- **Pain:** Ad-hoc SQL requests consumed ~20% of sprint time; analysts are bottleneck for business
- **Solution:** Plan-Execute multiagent pipeline — LLM writes SQL from natural language, validates, executes
- **Result:** Analytics team capacity expanded by ~20% per sprint
- **Status:** Shipped ✓

---

## Current objective

**Hypothesis discovery phase.** Find the next bank IT role where:
- There is a repetitive, measurable subtask consuming ≥15% of sprint time
- The subtask is rule-based or lookup-heavy (good AI fit)
- The team lead has pain awareness and can approve a pilot

**Validation timeline:** 2–4 weeks per hypothesis — 1–2 synthetic CustDev sessions first, then 3–5 real interviews to confirm or kill.

**Candidate roles — ranked by evidence × access (market scan done June 2026):**

| Role | Access | External evidence | Key metric | Rank |
|---|---|---|---|---|
| Data analysts (same team as DL-1) | **Have access** | DL-1 already shipped here | SQL pain solved; remaining pain = dashboards, Excel reports, analysis commentary | **#1** |
| Chatbot scenario writers | **Have access** | None external — DL-2b internal signal | 20% sprint waste on script fixes confirmed; utterance writing ~5-10% sprint additional | **#2** |
| QA engineers | No access yet | Strong — named pain "script fatigue" | State Street: 67% cut; DBS: 20 days → 1 | **#3** |
| Product Managers (digital channels — mobile app, internet banking) | No access yet — bridge via DL-1 analysts | Strong — direct RU bank case (Sovcombank: −50% PM routine); ChatPRD −60% PRD time | PRD↔implementation drift confirmed via synthetic CustDev; real interviews pending | **#4** |
| Product Designers (digital channels) | No access yet — bridge via PM relationship | Strong — 72% designers use gen AI (Figma State of Designer 2026); 78% UX teams use AI in research | Usability-test synthesis ("2 days" per test) confirmed via synthetic CustDev; blocked on PII review for test recordings | **#5** |

> **Note:** "Chatbot scriptwriters" and "scenario writers" are the same role — one person writes both JS scripts and NLU training data (intents, utterances, RegExp). DL-3 and DL-4 both target this role.

*Ranking logic: access is the binding constraint at <1 year tenure. QA has the strongest external evidence but no relationship — needs trust-building first. BA and scriptwriters can be interviewed now. PM and Designer sit in a separate digital-product org with no direct relationship yet — ranked below QA because, unlike QA's named external pain, their top hypotheses are only synthetic-CustDev-validated so far, and Designer additionally carries an unresolved PII question (usability-test recordings) that QA/PM don't.*

**Note on Scrum Masters:** Removed — they don't exist as a distinct role in this bank. Team leads double as SMs. The sprint reporting pain (30–120 min/sprint) is real but falls on team leads, not a separate role. Could surface as a secondary pain during team lead interviews.

**Market scan findings (June 2026):**
- QA "script fatigue" is a documented, named pain across Citi, HSBC, NatWest, Lloyds, Wells Fargo, DNB. AI-generated code is outpacing QA validation — 70–80% of devs use AI coding tools, QA adoption under 50%.
- Data analysts (DL-1 team): "Business analyst" in this bank = analytics role (SQL, dashboards, Excel) — NOT a requirements-writing BA. Same team as DL-1. SQL pain is already solved. Remaining pain is dashboard creation, Excel report generation, analysis commentary writing. This is an extension hypothesis, not a fresh role.
- Chatbot scriptwriter augmentation has zero published case studies externally. Either untapped or not yet done publicly.
- Roles out of scope: Data engineers (context-heavy, same failure mode as DL-2), Security/Antifraud (different department).
- Killed after synthetic CustDev: Intent coverage gap detection (needs conversation logs → PII constraint, hard blocker).

**→ Next actions:**
- **Done:** Market signal scan (June 2026)
- **Done:** Hypothesis generation + check + synthetic CustDev for Product Managers (DL-5) and Product Designers (DL-6) — July 7, 2026. Consolidated into `Hypotheses_AllRoles_23_26.md` (Роль 4 and Роль 5 sections) — the separate per-role files were merged in and removed.
- **Next:** Pick data analysts (DL-1 extension) or scriptwriters → run `skill-hypothesis-check.md` → open DL-3
  Suggested: Data analysts — existing relationship, SQL solved, now find the next bottleneck (dashboards / Excel / commentary)
- **Also queued:** DL-5 (PM — PRD generation from notes) and DL-6 (Designer — usability-test synthesis) need a warm intro into the digital-product org before live interviews can start; DL-6 additionally needs an infosec sign-off on processing usability-test recordings before its PoC can run.

**Out of scope:** DevOps/SRE/infrastructure roles; Security/Antifraud — separate department, no access.

See `## Decision Log` below for DL-2 (killed) and DL-2b (parked residual signal).

---

## Workflow (the core loop)

**One-time setup** *(already done for this product):*
- Fill in `CLAUDE_template.md` for a specific product → save as `CLAUDE.md`

**Per hypothesis cycle:**
0. **Generate candidates** using `skill-hypothesis-generating.md` — pull signals from market, CustDev, and product data → get a ranked list of 5–10 candidate hypotheses
1. Run the top candidate through `skill-hypothesis-check.md` → get a structured hypothesis + ICE score
2. Run a synthetic CustDev session using `skill-synthetic-custdev.md` → surface objections before real interviews
3. **Targeted market scan** using `skill-market-scan.md` → deep report on the specific hypothesis: TAM, players, trends, gaps — all with sources (different from step 0 — this is narrow, not broad)
4. Record the outcome in `skill-decision-log.md` → one `DL-N` entry per hypothesis cycle
5. Paste the DL-N entry into the `## Decision Log` section of `CLAUDE.md` → so the next session inherits context

One full cycle is ~3 hours. The loop is closed when the DL entry lives in `CLAUDE.md`.

## Files and their roles

| File | Role |
|---|---|
| `CLAUDE_template.md` | Product context template — fill this in per product and rename to `CLAUDE.md` |
| `skill-hypothesis-generating.md` | Generates hypothesis candidates from 3 sources (market, CustDev, product data) → prioritized list ready for hypothesis-check |
| `Hypotheses_WW_YY.md` | Cross-role hypothesis runs — one file per run (e.g. `Hypotheses_23_26.md`, `Hypotheses_23_26_2.md`). Latest: `Hypotheses_23_26_2.md` |
| `Hypotheses_AllRoles_23_26.md` | **Canonical, single source of truth** for all hypotheses across all 5 roles (44 total), in Russian — scriptwriters, analysts, QA, plus Product Managers (Роль 4, source for DL-5) and Product Designers (Роль 5, source for DL-6). All per-role files have been merged in and deleted; do not recreate separate per-role hypothesis files — add new roles as sections in this one file. |
| `skill-hypothesis-check.md` | Structures a raw idea into a testable hypothesis + ICE (1–10) + go/pivot/stop criteria |
| `skill-synthetic-custdev.md` | Turns Claude into a specific ICP persona for a practice interview session |
| `skill-market-scan.md` | Produces a structured market report: TAM, players, trends, gaps — all with sources |
| `skill-decision-log.md` | Template for recording what was tested, what was learned, and what the next step is |

## Using the skill files

Each `skill-*.md` contains a ready-made prompt block (marked with ` ``` `). Copy the prompt, fill in the `{placeholders}`, and paste into Claude. No installation required.

`skill-synthetic-custdev.md` works best when you give the persona 3–5 concrete personal details and an explicit pain. If the persona agrees with everything, the role is underspecified — add more friction.

`skill-market-scan.md` requires a tool with web search (Perplexity, Claude with web search, EXA, or Tavily). Without live search, AI will hallucinate market figures.

## Decision Log convention

Entries follow the format `DL-{N}`. Each entry must include a citation (quote or data point) — entries without evidence are not valid. **Exception:** parked hypotheses (not yet tested) may appear without evidence but must be labeled as untested. After each cycle, paste the new `DL-N` entry into the `## Decision Log` section below so future sessions see what was already tested.

---

## Decision Log

### DL-0 — RegExp Auto-Generator for chatbot scenario writers (Shipped)
**Hypothesis:** Scenario writers will recover ≥15% sprint capacity if given LLM-assisted RegExp generation from natural language intent descriptions.
**Test method:** Production deployment + sprint velocity measurement with full scenario-writing team.
**Evidence:** "30% sprint time recovered for scenario writers" — team lead estimate post-ship, not formally tracked. Directionally reliable, not independently verified.
**Decision:** Green — shipped and running. ✓

### DL-1 — Text→SQL multiagent system for data analysts (Shipped)
**Hypothesis:** Data analysts will expand sprint capacity if ad-hoc SQL requests are handled by a Plan-Execute LLM pipeline instead of manual query writing.
**Test method:** Production deployment + capacity measurement with full analytics team.
**Evidence:** "Analytics team capacity expanded by ~20% per sprint" — team lead estimate post-ship, not formally tracked. Directionally reliable, not independently verified.
**Decision:** Green — shipped and running. ✓

### DL-2 — Vibe coding tool for chatbot scriptwriters (Killed)
**Hypothesis:** Giving scriptwriters a vibe coding tool (Kilo Code) lets them stop writing code manually → non-technical hires replace expensive code-savvy people.
**Test method:** Several in-depth interviews + live pilot with one scriptwriter on Kilo Code.
**What we learned:**
1. Vibe coding tools perform poorly on context-heavy codebases, writing new functions, and consistent output quality.
2. Catching tool mistakes still requires understanding code — the skill requirement doesn't disappear.
3. Core assumption (non-technical person can own the output) is false with current tooling.
**Evidence:** "Catching tool mistakes still requires understanding code" — confirmed in live pilot.
**Decision:** Red — killed. Headcount-replacement angle is invalid with current AI tooling.

### DL-2b — Augment scriptwriters on script fixes (Parked — superseded by DL-3)
**Hypothesis (untested):** Existing scriptwriters can recover the confirmed 20% sprint waste on script fixes if given AI augmentation tools adapted to their codebase context — without requiring non-technical replacement hires.
**Why parked:** Superseded by DL-3, which tests a specific narrower angle (diagnosis-only) from the same residual signal.

---

### DL-3 — AI script defect diagnosis for chatbot scriptwriters (In Progress — opened June 4, 2026)

**Hypothesis:**
> Chatbot scriptwriters will reduce script-fix time by ≥50% if AI correctly identifies the root cause of a broken script from script + error log in ≥70% of cases — without writing or modifying code.

**Origin:** Residual signal from DL-2 interviews (20% sprint on fixes confirmed). Key insight: majority of fix time is diagnosis, not the fix itself (1h diagnosis / 15min fix ratio). Diagnosis-only scope avoids DL-2 failure mode (no code generation required → lower LLM quality bar).

**What we tested so far:**
- Method: Synthetic CustDev (persona simulation, June 4, 2026)
- Method: Market scan (June 2026) — no external case studies found for diagnosis-only tools in chatbot teams; angle appears untested publicly
- Method: Hypothesis-check + ICE scoring (June 4, 2026)

**What we learned so far:**
1. Pain confirmed real from DL-2 interviews — not an assumption
2. Synthetic CustDev confirmed: diagnosis time >> fix time ratio holds under pressure
3. Acceptance criterion handed by persona: test on already-fixed scripts — if AI diagnosis matches real root cause ≥70% of the time, trust is established
4. Key technical risk: self-hosted open-source LLM (LLaMA/Mistral) on large interconnected JS scripts — must scope to single-script input, not full codebase
5. Critical objection: "If wrong diagnosis >20-30% of the time, I stop trusting it and go back to manual"

**Evidence so far:**
> "Reading code and logs takes about an hour. The fix itself is usually 15 minutes." — Synthetic CustDev persona (grounded in DL-2 interview pattern)
> "20% sprint time on script fixes" — confirmed in real DL-2 interviews (not estimate)

**ICE:** I=8, C=7, A=8 → **448** (standardized to I·C·A per `skill-hypothesis-generating.md`; prior record was I=8,C=7,E=7→392 on the Effort axis)

**Validation still needed:**
- [ ] 3–5 live interviews with scriptwriters: confirm diagnosis/fix time split in real numbers
- [ ] Technical PoC: collect 10 already-fixed scripts + error logs, run LLM diagnosis, measure accuracy vs. real root causes

**Criteria:**
- **Green:** 3+ of 5 confirm diagnosis time >50% of fix time AND PoC accuracy ≥70% → build
- **Yellow:** Pain confirmed but PoC accuracy 50–70%, OR only 2/5 confirm → pivot: narrow to specific JS error types where LLM performs best
- **Red:** Fix time > diagnosis time for majority, OR PoC accuracy <50% → stop

**What to do next:**
- Next step: Schedule 3–5 interviews with scriptwriter team (warm contact from DL-2)
- Deadline: June 14, 2026 (10 days from opening)
- Responsible: Product owner

**Related:**
- Previous: DL-2 (killed), DL-2b (parked, superseded by this entry)
- Hypothesis born from: DL-2 residual signal (20% sprint on fixes)

---

### DL-4 — AI utterance generation for NLU training (In Progress — opened June 4, 2026)

**Hypothesis:**
> Scenario writers will recover ≥10% sprint capacity if AI generates diverse NLU training utterances from intent descriptions, reducing utterance-writing time from 1.5–2h per intent to under 30 minutes.

**Origin:** Adjacent unsolved pain on DL-0 team. DL-0 solved RegExp generation — utterance writing was always the next bottleneck. Pattern: every shipped product leaves 2–3 adjacent pains on the same team. Confirmed by synthetic CustDev that utterances take 1.5–2h per intent with 2–4 intents per sprint.

**What we tested so far:**
- Method: Synthetic CustDev (persona simulation, June 4, 2026)
- Method: Hypothesis-check + ICE scoring (June 4, 2026)
- Method: Run 2 hypothesis generation — confirmed as top candidate from 10 new hypotheses

**What we learned so far:**
1. Pain: 1.5–2h per intent × 2–4 intents/sprint = 3–8h/sprint on utterances alone (~5–10% sprint)
2. DL-0 trust transfers directly — same team, same "describe → generate → review" pattern
3. Key risk #1: Output diversity — repetitive utterances harm NLU model quality more than none
4. Key risk #2: Domain-specific intents (mortgages, payments) — AI may lack bank-specific terminology
5. Key risk #3: Russian language quality — unnatural phrasing is worse than manually written utterances
6. Acceptance bar is low: "I describe the intent, it gives examples, I review" — same workflow as DL-0

**Evidence so far:**
> "Every sprint we have 2–4 new intents. Utterances are still fully manual — the boring part of the job." — Synthetic CustDev persona (grounded in DL-0 team context)
> "RegExp generator saved a lot — but utterances are still fully manual." — Synthetic CustDev persona

**ICE:** I=7, C=7, E=8 → **392**

**Validation still needed:**
- [ ] 3–5 live interviews with DL-0 scenario writers: confirm utterance time and sprint frequency
- [ ] Language quality test: generate 50 utterances for a real bank intent, have a scenario writer grade diversity + naturalness
- [ ] Domain test: pick a bank-specific intent (e.g. "early mortgage repayment"), check if LLM output is usable

**Criteria:**
- **Green:** 3+ of 5 confirm utterance writing >1h per intent AND language quality test passes writer review ≥70%
- **Yellow:** Pain confirmed but Russian quality or diversity below threshold → pivot: human-in-the-loop editing step, generate 30 drafts → writer selects + edits best 20
- **Red:** Utterance writing <30 min per intent (pain too small) OR output quality unacceptable after editing → stop

**What to do next:**
- Next step: Interview DL-0 team — warm contact, same team as RegExp generator pilot
- Parallel: Run a quick language quality test with 1 real intent before interviews (2h dev work)
- Deadline: June 14, 2026
- Responsible: Product owner

**Related:**
- Previous: DL-0 (shipped — RegExp generation for same team)
- Born from: DL-0 adjacent pain, Hypotheses_23_26_2.md run 2 top candidate
- Running in parallel with: DL-3 (same scriptwriter team, different pain)

---

### DL-5 — AI PRD generation for bank Product Managers (In Progress — opened July 7, 2026)

**Hypothesis:**
> Product Managers of digital channels (mobile app, internet banking) will cut PRD drafting friction and PRD↔implementation drift if AI generates a traceable PRD draft from call notes and idea descriptions, provided every line can be traced back to its source and no requirement is invented.

**Origin:** New role, opened via `skill-hypothesis-generating.md` full 3-source run (market + synthetic CustDev + vision). First hypothesis cycle for this role — no prior DL history.

**What we tested so far:**
- Method: Market scan (July 7, 2026) — direct RU bank case study found (Sovcombank), plus ChatPRD/industry adoption data
- Method: Synthetic CustDev (persona simulation, July 7, 2026) — two passes: general workflow discovery, then objection-focused deep dive on this specific hypothesis
- Method: Hypothesis-check + ICE scoring (July 7, 2026)
- Method: Live interviews — **guides prepared, interviews not yet conducted** (July 7, 2026). Split by specialization since "digital-channel PM" covers three distinct teams:

| Специализация | Гайд | Статус |
|---|---|---|
| Мобильное приложение | `Interview_ProductManagers_06_26_Mobile.md` | Не проведено — ждём тёплого интро через тимлида DL-1 |
| Интернет-банк (веб) | `Interview_ProductManagers_06_26_Web.md` | Не проведено — ждём тёплого интро через тимлида DL-1 |
| Голосовые/чат-помощники | `Interview_ProductManagers_06_26_Voice.md` | Не проведено — доступ короче (мост через команду DL-0/DL-3/DL-4), но интро тоже пока не запрошено |

> Ни одно из трёх интервью пока не даёт реальных цитат/цифр — секция «Evidence so far» ниже содержит только рыночные и синтетические данные (уже помечены как таковые). Когда интервью пройдут, для каждой специализации нужно добавить отдельный блок «Что узнали» + «Цитаты» по шаблону `skill-decision-log.md`, а не переписывать общий вывод по всем трём сразу — специализации могут дать разный результат (см. кросс-ссылки в самих гайдах).

**What we learned so far:**
1. Pain is real in the synthetic persona but narrower than the market case suggests: PRD writing itself is "not painful, just slow" — the actual pain is PRD↔implementation drift (decisions made in chat/calls never make it back into the document) and executive-summary writing for committee reports
2. Direct RU competitor evidence: Sovcombank shipped a full-cycle PM AI assistant and reported ~50% routine-time reduction — strongest external signal of any new-role hypothesis so far, but scope is dangerously broad (see risk below)
3. Key risk — repeats DL-2 failure mode if unscoped: a "full product-cycle assistant" (documentation + prioritization + analytics + GTM, as in the Sovcombank case) is too broad and hard to measure; must be cut narrow like DL-3/DL-4, not copied wholesale
4. Critical objection from persona: accountability — "so the AI generated it" is not an acceptable answer to a compliance/architecture question; every PRD line must be traceable to its source note
5. Critical objection: a self-hosted-only constraint is non-negotiable here — external SaaS tools (ChatPRD and similar from the market signal) would need months of infosec approval and are out of scope from day one
6. Critical objection: tolerance for hallucinated requirements is close to zero — one bad requirement reaching development erases all time savings and triggers full manual re-review going forward

**Evidence so far:**
> "ИИ-ассистент... сократил рутину продуктовой команды на 50%" — Sovcombank Technologies, published case study (RU bank, direct competitor context)
> "PM сократил время написания PRD на 60% используя ChatPRD" — ChatPRD 2026 guide (external, cloud-tool context, not yet verified on our self-hosted stack)
> "Через месяц у PRD и у того, что реально запилили, расхождение — потому что решения принимались в переписке, а не в документе" — synthetic CustDev persona
> "Если хоть раз в разработку уйдёт требование, которого не было — я после этого буду перечитывать каждую строчку так же внимательно, как если бы писала сама" — synthetic CustDev persona (objection-focused session)

**ICE:** I=7, C=7, E=6 → **294** (I·C·A synthesis score in the source doc: I=7, C=7, A=4 → 196; A reflects no direct access yet, bridged only via DL-1 analysts)

**Validation still needed:**
- [ ] Warm intro via DL-1 analytics team lead to a digital-channel PM (mobile + web) — no separate bridge exists for these two yet
- [ ] Warm intro via DL-0/DL-3/DL-4 scriptwriter team lead to the voice/chat-assistant PM — shorter path, not yet requested
- [ ] Run `Interview_ProductManagers_06_26_Mobile.md` (3–5 respondents) — confirm PRD↔implementation drift as regular, not occasional, in real numbers
- [ ] Run `Interview_ProductManagers_06_26_Web.md` (3–5 respondents) — same, currently only transferred by analogy from the mobile synthetic CustDev, not independently confirmed
- [ ] Run `Interview_ProductManagers_06_26_Voice.md` (3–5 respondents) — same, plus confirm PM notes don't routinely contain unmasked customer dialogue fragments
- [ ] Technical PoC: 5–10 real (anonymized) PRDs + call notes, run on self-hosted LLM, measure share of correctly traced sections vs. invented requirements
- [ ] Confirm self-hosted-only constraint is acceptable to infosec before any external tool is even considered

**Criteria:**
- **Green:** 3+ of 5 PMs confirm PRD↔implementation drift as a regular problem AND PoC traceable-coverage ≥85–90% with zero invented requirements → build (draft-with-traceability + confidence markers, not an autonomous full-cycle assistant)
- **Yellow:** Pain confirmed but PoC accuracy 70–85% or hallucination rate meaningful → pivot: every generated line ships with an explicit low-confidence flag; PM reviews flagged lines only
- **Red:** PMs write PRDs in under 1h with no drift problem, OR self-hosted LLM invents requirements at a rate the persona's zero-tolerance bar rejects → stop

**What to do next:**
- Next step: Request warm intro from DL-1 team lead (mobile + web PM) and from DL-0/DL-3/DL-4 team lead (voice PM) — voice has the shorter path, try it first
- Deadline: 3–4 weeks (wider than typical cycle — new org, no existing warm contact for two of the three specializations)
- Responsible: Product owner

**Related:**
- Full hypothesis run: `Hypotheses_AllRoles_23_26.md`, Роль 4 (7 candidates generated, top-3 checked, top-1 deep synthetic CustDev)
- Interview guides (prepared, not yet run): `Interview_ProductManagers_06_26_Mobile.md`, `Interview_ProductManagers_06_26_Web.md`, `Interview_ProductManagers_06_26_Voice.md`
- Cautionary parallel: DL-2 (killed) — do not repeat "full-cycle assistant" scope creep
- Running in parallel with: DL-6 (same digital-product org, adjacent role — Product Designer)

---

### DL-6 — AI usability-test synthesis for bank Product Designers (In Progress — opened July 7, 2026)

**Hypothesis:**
> Product Designers of digital channels will cut usability-test analysis time from ~2 days to ≤0.5 day per test if AI extracts themes with verbatim quotes and exact timestamps from test recordings, provided quotes are checkably accurate (not paraphrased) and sensitive data (card numbers, amounts spoken during the test) is masked before the transcript reaches any LLM.

**Origin:** New role, opened via `skill-hypothesis-generating.md` full 3-source run (market + synthetic CustDev + vision). First hypothesis cycle for this role — no prior DL history.

**What we tested so far:**
- Method: Market scan (July 7, 2026) — strong external adoption data (Figma State of the Designer 2026, AI UX research tooling category)
- Method: Synthetic CustDev (persona simulation, July 7, 2026) — two passes: general workflow discovery, then objection-focused deep dive on this specific hypothesis
- Method: Hypothesis-check + ICE scoring (July 7, 2026)

**What we learned so far:**
1. Pain confirmed as the single most emotionally intense pain in the persona session: ~2 days of manual work per usability test (watch 5–6 recordings + synthesize into a citable document)
2. Market context is strong but transfers via cloud SaaS (Dovetail, Perspective AI, Miro Assist) — this role's central risk is data perimeter, not model quality, unlike every other role tested so far (DL-0/DL-1/DL-3/DL-4 inputs are text-only; this role's input is audio/video of real bank customers)
3. Critical objection: usability-test scripts routinely include real payment scenarios ("show me how you normally pay") — participants say amounts and show card fragments on screen. This is a structural PII risk built into the test format itself, not a hypothetical edge case
4. Critical objection: quotes must be verbatim with exact timestamps because designers use them as evidence in front of PM/dev — paraphrasing or timestamp drift makes the output useless even if the theme is correct
5. Critical objection: audio-only transcripts lose non-verbal signal (pauses, hesitation, repeated mis-taps) that audio-with-video would capture, but video sharply raises data sensitivity (customer faces) — a real tradeoff with no clean answer
6. Same "one failure, zero savings" trust threshold as DL-5: a single inaccurate synthesis sends the designer back to full manual review, now with an added verification step

**Evidence so far:**
> "72% дизайнеров используют генеративный ИИ в работе, 98% нарастили использование год к году" — Figma State of the Designer 2026
> "78% UX/продуктовых команд используют ИИ в исследовательских процессах (рост с 34% в 2024)" — Maze State of UX Research 2026, via Storyflow
> "Пять записей по 40 минут — это почти целый день только на просмотр, плюс ещё день, чтобы свести в внятные выводы" — synthetic CustDev persona
> "Записи юзабилити-тестов — это голоса и лица реальных пользователей банка... сами респонденты иногда называют номера карт или суммы вслух" — synthetic CustDev persona (objection-focused session)

**ICE:** I=7, C=6, E=5 → **210** (I·C·A synthesis score in source doc: I=7, C=7, A=3 → 147; A reflects no direct access — bridge only via the PM relationship being built under DL-5)

**Validation still needed:**
- [ ] Infosec check: is processing usability-test audio (even with number-masking) permissible on the self-hosted contour? This is a harder blocker than in any prior DL and must clear before a PoC is worth running
- [ ] Warm intro via a digital-channel PM (once DL-5 relationship exists) to a lead Product Designer
- [ ] 3–5 live interviews: confirm ~2-day analysis time and the verbatim-quote trust bar in real numbers
- [ ] Technical PoC: 3–5 anonymized/navigation-only test recordings (no real payment scenarios) → transcript + number-masking → LLM synthesis → compare extracted quotes/timestamps against the designer's own manual analysis of the same recordings

**Criteria:**
- **Green:** 3+ of 5 designers confirm >1 day per test AND PoC quote accuracy ≥90% on anonymized data with infosec clearance obtained → build (audio-only + number-masking scope, not video)
- **Yellow:** Pain confirmed but masking destroys too much context (accuracy 70–90%), OR infosec allows only a restricted subset of test types → pivot: audio-only, human does a final quote-verification pass before anything is shared as "evidence"
- **Red:** Infosec blocks processing usability-test recordings even when anonymized, OR accuracy <70% → stop

**What to do next:**
- Next step: Raise the infosec question about usability-test recording processing before committing further design-partner time
- Parallel: Pursue the DL-5 PM relationship as the access bridge into the design team
- Deadline: 3–4 weeks (wider than typical cycle — new org, no warm contact, added infosec gate)
- Responsible: Product owner

**Related:**
- Full hypothesis run: `Hypotheses_AllRoles_23_26.md`, Роль 5 (7 candidates generated, top-3 checked, top-1 deep synthetic CustDev)
- Running in parallel with: DL-5 (same digital-product org, adjacent role — Product Manager, serves as access bridge)
