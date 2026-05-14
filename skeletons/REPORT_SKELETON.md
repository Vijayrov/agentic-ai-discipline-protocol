# <Report ID>-REPORT

**Prompt:** <prompt-ID>
**Executed:** <ISO 8601 UTC timestamp>
**Files modified:** <list with line ranges, OR "none — read-only">
**Tests run:** <command + result; test baseline verification if code touched>

## Executive summary

<1–3 sentences, verdict-level only. No narrative.>

---

## Task 1 — <name>

**Verdict:** <one sentence>

**Evidence:**

- **VERIFIED** — <citation: file path + line ref + verbatim quote of relevant content. For substrate/curriculum writes per INV-11, cite the upstream source backing the value PER-WRITE, not header-only.>
- **INFERRED** — <rationale + what would verify>
- **HYPOTHESIS** — <statement + what would test it>

---

## Task 2 — <name>

**Verdict:** <one sentence>

**Evidence:**

- **VERIFIED** — <citation>
- **INFERRED** — <rationale>

---

## Strategic flags raised

List each trigger from the prompt individually with NOT FIRED / FIRED status + evidence:

| Trigger | Status | Evidence |
|---------|--------|----------|
| <Trigger 1 from prompt> | NOT FIRED | <verbatim citation showing trigger condition not met> |
| <Trigger 2 from prompt> | FIRED | <what triggered, what was halted, what remains executable> |
| <Trigger 3 from prompt> | NOT FIRED | <citation> |

Do NOT consolidate triggers into generic categories.

---

## Open questions

For Orchestrator or Human:

1. <question — uncertainty goes here, not in findings as a soft claim>
2. <question>

---

## Success criterion evidence

<≥50 chars, concrete, citation-backed. Not "task completed successfully" — that's trivially affirmative and fails Gap 9.>
