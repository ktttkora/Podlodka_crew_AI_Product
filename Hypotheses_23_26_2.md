# Hypotheses — Week 23, 2026 (Run 2)

**Generated:** June 4, 2026
**Skill used:** `skill-hypothesis-generating.md` (all 3 sources + synthesis)
**Previous run:** `Hypotheses_23_26.md` — all 10 hypotheses from run 1 excluded from this run

---

## Sources this run

| Source | Input |
|---|---|
| **Market** | NLU training data tools; code review AI in fintech; requirements/spec writing assistants; meeting intelligence; unit test generation tools |
| **CustDev** | Adjacent pains from DL-0 team (utterances unsolved after RegExp); DL-1 team (SQL documentation debt, anomaly investigation); DL-3 team (prevention vs. cure angle) |
| **Vision** | Pattern: every DL leaves adjacent unsolved pain on same team. System analysts (ТЗ writers) exist in Russian banks as distinct role. DL-3 targets diagnosis — prevention angle untested. |

---

## Raw candidates before scoring

| # | Hypothesis | Role | Sources |
|---|---|---|---|
| 1 | AI generates NLU training utterances from intent description | Scenario writers (DL-0 team) | CustDev ★ Vision |
| 2 | AI detects conflicting/overlapping intents in the library | Scenario writers (DL-0 team) | Vision ★ Market |
| 3 | AI generates test dialogues from existing scenario logic | Scenario writers (DL-0 team) | Vision |
| 4 | AI explains complex SQL queries for documentation/handoffs | Data analysts (DL-1 team) | Vision |
| 5 | AI generates ТЗ (technical spec) sections from business requirements | System analysts | Market ★ Vision |
| 6 | AI reviews script changes before push to production | Scriptwriters (DL-3 team) | Vision ★ Market |
| 7 | AI drafts anomaly investigation brief when data alert fires | Data analysts (DL-1 team) | Vision |
| 8 | AI generates unit tests from function specification | Backend developers | Market |
| 9 | AI writes test environment setup documentation | QA | Market |
| 10 | AI extracts meeting minutes and action items from notes | Any IT team | Market |

---

## Priority Table (pre-synthetic)

| # | Hypothesis | I | C | A | Score | Sources |
|---|---|---|---|---|---|---|
| 1 | Utterance generation for NLU training | 7 | 7 | 8 | **392** | CustDev ★ Vision |
| 5 | ТЗ section generation for system analysts | 7 | 6 | 4 | **168** | Market ★ Vision |
| 6 | Pre-push script code review | 7 | 6 | 8 | **336** | Vision ★ Market |
| 7 | Anomaly investigation brief | 6 | 6 | 9 | **324** | Vision |
| 2 | Intent conflict detection | 6 | 6 | 8 | **288** | Vision ★ Market |
| 3 | Test dialogue generation | 6 | 5 | 8 | **240** | Vision |
| 4 | SQL explanation for handoffs | 5 | 6 | 9 | **270** | Vision |
| 8 | Unit test generation (backend devs) | 7 | 5 | 2 | **70** | Market |
| 9 | Test environment docs (QA) | 4 | 5 | 2 | **40** | Market |
| 10 | Meeting minutes extraction | 5 | 5 | 5 | **125** | Market |

---

## Synthetic CustDev — All 10

---

### #1 — Utterance generation for NLU training
**Persona:** Scenario writer, DL-0 user, creates NLU training data

**Q: How do you populate utterances when you add a new intent?**
A: "Manually. You need 50-100 different ways users might say the same thing. I sit and invent them one by one. For a complex intent it takes 1.5-2 hours. The boring part of the job."

**Q: Is this a regular sprint task?**
A: "Every sprint we have 2-4 new intents. So yes, this is a real time sink. RegExp generator (DL-0) saved a lot — but utterances are still fully manual."

**Q: If AI generated utterance drafts from your intent description?**
A: "I'd use it. Similar to the RegExp tool. I describe the intent, it gives me examples, I review and edit. The key question is Russian quality — we have users who write in different styles, slang, abbreviations."

**Q: What would stop you?**
A: "Repetitive outputs. If it generates 50 near-identical variations I'm back to doing it myself. Needs real diversity. And some intents are highly domain-specific — 'cancel mortgage early repayment' — I'm not sure AI knows enough about that."

**Q: Who approves?**
A: "Team lead. Same as DL-0. If I show it works on 1-2 intents first, I think it's an easy yes."

**Confirmed:** 1.5-2h per intent, 2-4 intents/sprint = 3-8h/sprint on utterances alone (~5-10% sprint). DL-0 trust transfers.
**New objection:** Diversity of outputs — repetitive utterances are worse than none (harm NLU model quality).
**New objection:** Domain-specific intents (mortgage, payments) — AI may not know bank terminology well enough.
**Verdict: ✅ CONFIRMED. Strongest hypothesis of this batch.**

---

### #2 — Intent conflict detection
**Persona:** Scenario writer managing 200+ intent library

**Q: Do you have conflicts between intents?**
A: "Yes. As the library grows, new intents start overlapping with old ones. NLU model gets confused, misroutes happen."

**Q: How do you detect this now?**
A: "Reactively — support flags misroutes. Or we notice during model retraining when two intents compete for examples."

**Q: If AI scanned the library and flagged overlapping intents?**
A: "Useful for quarterly reviews. But we also have intentional similarity — some intents are designed to handle variations of the same request. AI would need to understand that difference."

**Q: How often is this a sprint-level task vs occasional?**
A: "Mostly occasional. It's not like I'm checking for conflicts every sprint. Maybe once a quarter formally, or when something breaks."

**Low sprint frequency confirmed.** Quarterly task = not a sprint-level pain.
**Verdict: ⚠️ VALID BUT LOW FREQUENCY. Better as a monitoring tool than a sprint hypothesis.**

---

### #3 — Test dialogue generation
**Persona:** Scenario writer who QAs chatbot releases

**Q: How do you test before a release?**
A: "We write test dialogues — cover main flows and edge cases. For big releases it takes a day."

**Q: If AI generated test dialogue drafts from your scenario scripts?**
A: "Could work if it uses our own intents and RegExp patterns. Not random inputs — inputs that match what our NLU model is trained on."

**Q: What would stop you?**
A: "Coverage gaps. If AI generates only happy-path dialogues and skips edge cases, we'll miss real bugs. Also the dialogue needs to match our tone — not robotic test inputs."

**Q: Is this more or less painful than utterance writing?**
A: "Less. Test dialogues happen before each release — maybe biweekly. Utterances are every sprint. The math is different."

**Lower frequency than utterances.** Extension of DL-0 output (using existing RegExps as input) is a real technical angle.
**Verdict: ⚠️ REAL BUT LESS URGENT THAN #1. Second priority for scenario writer track.**

---

### #4 — SQL explanation for handoffs
**Persona:** DL-1 analyst with complex undocumented SQL

**Q: Do you document your SQL queries?**
A: "No. We should. We don't have time. When someone needs to understand a query they ask me."

**Q: Is this painful?**
A: "When I'm on leave and someone breaks something — yes. Or when a new analyst joins. They spend days understanding the query logic."

**Q: If AI explained a query in plain language after you wrote it?**
A: "Easy to try. SQL is structured, AI should handle it. I'd run it once per query. Even a partial explanation is better than nothing."

**Q: Does this actually block sprint work?**
A: "Not actively. It's chronic background pain that surfaces during handoffs — maybe once a month."

**Verdict: ❌ CHRONIC, NOT ACUTE. No sprint-level urgency. Better as a background feature bundled with DL-1 than a standalone hypothesis.**

---

### #5 — ТЗ section generation for system analysts
**Persona:** System analyst writing technical specifications (ТЗ) for new features (hypothetical — no current relationship)

**Q: What takes most of your time when writing a ТЗ?**
A: "Structuring it. Each ТЗ has 15-20 standard sections. Half of them are the same across every document — scope, terms, regulatory references. I copy-paste and edit. The unique parts are the functional requirements."

**Q: How long per ТЗ?**
A: "2-3 days for a full one. The copy-paste sections alone take half a day."

**Q: If AI generated the standard sections from context?**
A: "Would save time on the boilerplate. But every bank has their own ТЗ standard — GOST or internal. AI would need to know our specific template."

**Q: Who are you in the org? Do I have a path to you?**
A: "I'm in the development department. We work alongside dev teams."

**Pain is real.** Template-heavy, copy-paste work = good AI fit. But no existing relationship. Different team.
**Verdict: ⚠️ REAL PAIN, NO ACCESS. Add to access-building track. High potential when relationship opens.**

---

### #6 — Pre-push script code review
**Persona:** Scriptwriter from DL-3 team

**Q: Do you review your changes before pushing?**
A: "I look things over. Quick check. But it's fast — I mostly trust myself at this point."

**Q: Would an AI code review before push be useful?**
A: "Maybe. But I'd need it to be automatic — not something I manually run. And it would need to understand our platform's specific patterns, not just generic JS."

**Q: Is this more valuable than the diagnosis tool (DL-3)?**
A: "Less urgent. Fixing broken scripts is already a real problem I deal with every sprint. Prevention is nice but not burning."

**Q: What would stop you?**
A: "False positives. If it flags things that are actually fine, I'll ignore it completely. Better no review than a noisy one."

**"Less urgent than DL-3" confirmed by persona.** Nice-to-have, not need-to-have. Requires platform-specific training.
**Verdict: ❌ NICE-TO-HAVE. Bundle with DL-3 as phase 2 feature, not standalone hypothesis.**

---

### #7 — Anomaly investigation brief
**Persona:** DL-1 analyst who receives data anomaly alerts

**Q: When you get an anomaly alert, what do you do?**
A: "I look at the data, try to understand if it's real or a data issue. Pull related metrics, look at what changed. Write up a quick explanation for the team."

**Q: How long does this take?**
A: "30 minutes to an hour usually. Sometimes longer if the cause isn't obvious."

**Q: How often does this happen?**
A: "2-3 times per week. Some weeks more if we're in a data-heavy sprint."

**Q: If AI drafted the initial investigation brief — here's the anomaly, here's what changed around it, here are possible causes?**
A: "That would actually save time. Most anomalies follow patterns — sudden drop usually means data pipeline issue or an event. If AI gave me a starting point with possible explanations, I'd refine rather than start from scratch."

**Q: What would stop you?**
A: "Hallucinated causes. If AI invents explanations with confidence, I might chase the wrong thing. Needs to distinguish 'likely cause' from 'possible cause' from 'I don't know'."

**Pain confirmed:** 30-60 min × 2-3/week = up to 3h/week = ~4% sprint. Not huge alone but real.
**Interesting angle:** Starting point vs blank page. Analyst refines, doesn't verify from scratch.
**Risk:** Hallucinated confident explanations.
**Verdict: ✅ REAL. Lower than #1 but worth keeping. Third slot candidate.**

---

### #8 — Unit test generation (Backend developers)
**Persona:** Backend developer (hypothetical — no access, out of main scope)

**Q: Do you write unit tests?**
A: "Yes. It takes time. A good test suite for a new function can take as long as writing the function itself."

**Verdict: ❌ OUT OF SCOPE + NO ACCESS. Backend developers are not in current focus. Drop.**

---

### #9 — Test environment setup documentation (QA)
**Persona:** QA engineer (hypothetical — no access)

**Q: Do you document test environment setup?**
A: "Badly. It's always out of date. Onboarding a new QA person takes days because of this."

**Verdict: ❌ NO ACCESS + WRONG PROBLEM. Documentation debt is real but not a sprint bottleneck. Drop.**

---

### #10 — Meeting minutes and action item extraction
**Persona:** Any IT team member after a meeting

**Q: Do you write meeting minutes?**
A: "Sometimes. More often we have a chat message with decisions. Formal minutes — rarely."

**Q: Is this a real pain?**
A: "It's annoying but we've adapted. We use chat for everything. Minutes are mostly ceremonial."

**Q: What about action items — do they get lost?**
A: "Sometimes. But that's a process problem more than a tool problem."

**Verdict: ❌ ACCEPTED PAIN, PROCESS PROBLEM. Not a sprint-time bottleneck. Generic enterprise tool already exists (Teams/Zoom AI). Drop.**

---

## Post-Synthetic Re-Ranking

| # | Pre-synthetic score | Synthetic verdict | Final status |
|---|---|---|---|
| #1 Utterance generation | 392 | ✅ Confirmed. 5-10% sprint, warm access, DL-0 trust | **TOP 3 — #1** |
| #7 Anomaly investigation brief | 324 | ✅ Real. 4% sprint, DL-1 team, starting-point angle | **TOP 3 — #2** |
| #2 Intent conflict detection | 288 | ⚠️ Valid but quarterly, not sprint-level | **TOP 3 — #3 (conditional)** |
| #3 Test dialogue generation | 240 | ⚠️ Real but less urgent than #1 | Next after top 3 |
| #5 ТЗ system analysts | 168 | ⚠️ High potential, no access | Access-building track |
| #6 Pre-push code review | 336 | ❌ Nice-to-have, bundle with DL-3 | Drop / DL-3 phase 2 |
| #4 SQL explanation | 270 | ❌ Chronic, not acute | Drop / DL-1 feature |
| #8 Unit test gen | 70 | ❌ Out of scope + no access | Drop |
| #9 Test env docs | 40 | ❌ No access + wrong problem | Drop |
| #10 Meeting minutes | 125 | ❌ Accepted pain, generic tools exist | Drop |

---

## Top 3 for Real-World Validation

**#1 — Utterance generation for NLU training (Scenario writers, DL-0 team)**
Score: 392 | Access: ✅ Warm | Sources: CustDev ★ Vision

Pain: 1.5-2h per intent × 2-4 intents/sprint = 3-8h/sprint on utterances alone.
DL-0 creates direct trust transfer — same team, same pattern (describe → generate → review).
Key risk: output diversity and Russian language domain quality.
First interview question: *"После того как сделали RegExp генератор — что теперь занимает больше всего времени при создании нового интента?"*

**#2 — Anomaly investigation brief (Data analysts, DL-1 team)**
Score: 324 | Access: ✅ Warm | Sources: Vision

Pain: 30-60 min per anomaly × 2-3/week = up to 3h/week, ~4% sprint.
DL-1 trust transfer — same team, existing positive AI experience.
Unique angle: AI provides starting point with possible causes ranked by likelihood, not a full explanation.
Key risk: hallucinated confident causes → must communicate uncertainty clearly.
First interview question: *"Когда приходит алерт об аномалии в данных — опиши первые 30 минут: что ты делаешь?"*

**#3 — ТЗ section generation for system analysts (System analysts)**
Score: 168 pre-synthetic | Access: ⚠️ No path yet | Sources: Market ★ Vision

Pain: half a day per ТЗ on boilerplate sections = significant. Very template-heavy = excellent AI fit.
Not in current access map — needs a warm intro. But pain pattern is the strongest match to the validated formula in this batch.
Action: ask DL-1 or DL-0 team leads if they work with system analysts. One warm intro unlocks this.
First interview question: *"Как выглядит процесс написания ТЗ — какая часть документа шаблонная, а какая требует реального мышления?"*

---

## Structural insight from this run

All three confirmed hypotheses cluster around **teams we already have access to** (DL-0 and DL-1) — same pattern as run 1. The access constraint is the binding variable, not idea quality. ТЗ analysts (#3) break that pattern and have the strongest pain match — worth one warm intro attempt before the next hypothesis cycle.

**Pattern emerging across both runs:**
Each shipped product (DL-0, DL-1) leaves 2-3 adjacent unsolved pains on the same team. The fastest path is not finding new roles — it's going deeper on teams where trust already exists.

---

*Generated using `skill-hypothesis-generating.md` (Run 2)*
*Sources: Market (NLU tools, code review AI, spec writing tools), CustDev (DL-0/DL-1/DL-3 adjacent signals), Vision (extension pattern)*
*Run 1 reference: `Hypotheses_23_26.md`*
*Synthetic CustDev run: June 4, 2026*
