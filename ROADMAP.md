# AADP Roadmap

**Status as of 2026-05-15.** This document tracks candidate features and amendments for future AADP versions. Inclusion as a candidate is not a commitment to ship. Promotion criteria require operational evidence.

---

## Current version

**v1.0** — tagged 2026-05-14. Initial public release. 11 anti-hallucination invariants, 3-role architecture (chat-Claude, coder, human decision-maker), versioned substrate, failure-mode escalation pattern. Validated in production via the MAYA project (anonymised case study in `case-studies/MAYA_anonymized.md`).

---

## v1.1 — Candidate features

Amendments accumulating from operational evidence post-v1.0. Promotion to LOCKED status requires ≥3 cycles of operational evidence. v1.1 ships when ≥3 candidates are LOCKED.

### v1.1-C1 — Verbatim diff for substrate transcription tasks

**Status:** CANDIDATE
Amendment to §3 report contract: substrate transcription tasks must include verbatim `diff` output proving no unintended modifications.

### v1.1-C2 — Verbatim source quoting for executable-code creation

**Status:** CANDIDATE
Amendment to §3 report contract: executable-code creation tasks must include verbatim quotes of critical function bodies.

### v1.1-C3 — INV-1 reinforcement: auto-detected = INFERRED

**Status:** CANDIDATE
Amendment to §4: auto-detected, pattern-matched, or search-discovered values are INFERRED, not VERIFIED. VERIFIED requires explicit human-locked source.

### v1.1-C4 — Task 0 Path Resolution skeleton addition

**Status:** PILOTING
Amendment to §6: implementation prompts include Task 0 to verify all referenced paths against disk before any work begins.

### v1.1-C5 — Task 0 Pre-Flight for remediation prompts

**Status:** PILOTING
Amendment to §6: remediation prompts include a pre-flight that quotes the prior report verbatim.

### v1.1-C6 — Release-anchor facts in human-locked config

**Status:** CANDIDATE
Architectural principle: version state and release-anchor facts (current_version, last_release_date, baseline_floor) must live in human-authority config fields, never auto-detected.

### v1.1-C7 — INV-12: SHA-256 read fingerprinting

**Status:** PILOTING
New invariant for §4: every file read by an agent during a prompt produces a SHA-256 hash, captured at read-time, reported in an "Inputs read" block. Cryptographic anchor for INV-3 (verbatim) and INV-10 (pre-action read). §3 amended to require the block.

### v1.1-C8 — Parsing anchored on stable identifiers

**Status:** CANDIDATE
Discipline note: parsing logic must anchor on stable identifiers (locked decision IDs, schema versions, explicit named fields), never on free-text patterns that recent writes may have inserted. Prevents self-referential parsing bugs.

---

## v2.0 — Architectural candidates

Major-version candidates requiring architectural change, not refinement. Promotion to LOCKED status requires ≥20 cycles of production evidence per the new mechanism.

### v2.0-C1 — Critic agent (fourth role)

**Status:** CANDIDATE
Add an adversarial Critic-Claude as a fourth role. Reads coder reports before they reach the human decision-maker. Hunts for INV-1 through INV-11 violations. Surfaces flags. Never executes, never decides. Mapped to the ColMAD (Collaborative Multi-Agent Debate) literature pattern (arXiv 2510.20963, October 2025).

**Promotion criterion:** Critic agent runs in parallel on ≥20 production cycles; demonstrates non-zero catch rate of violations that human audit would have missed.

### v2.0-C2 — Structured substrate with schema validation

**Status:** CANDIDATE
Migrate DECISIONS.md, SESSION_STATE.md, and other substrate files from markdown prose to structured JSON-with-schema. CI hook enforces INV-11 source-citation at write-time, not audit-time.

**Promotion criterion:** Schema operational for ≥50 cycles; ≥1 instance where the schema catches a violation that the previous prose pattern missed.

### v2.0-C3 — Calibrated confidence labels

**Status:** CANDIDATE
Extend INV-1 from three states (VERIFIED, INFERRED, HYPOTHESIS) to four-state with numeric confidence band (VERIFIED-0.95, INFERRED-0.7, HYPOTHESIS-0.3, ABSTAIN). Track calibration over time. Apply selective-prediction discipline.

**Promotion criterion:** Confidence band tracked across ≥100 claims; documented calibration drift or stability.

### v2.0-C4 — Release-Monitor-Claude (RMC)

**Status:** PILOTING
Daily-run substrate observer that applies version-bump criteria from `version_rules.json` and emits a verdict file. Already implemented and running on the reference instance (MAYA workspace) as of 2026-05-15. Pilot continues for 30-day shakeout.

**Promotion criterion:** 30 consecutive daily runs with no false MAJOR-CANDIDATE or MINOR-CANDIDATE emissions; demonstrated correct flagging when criteria are met.

### v2.0-C5 — AQL sampling regime for audits

**Status:** CANDIDATE
Once a maintainer's substrate is in statistical control, transition from 100% audit to AQL-style sampling per Lean Six Sigma DOE principles. Frees attention budget for high-value review.

**Promotion criterion:** Documented statistical-control evidence on the prior 30+ cycles; defined sampling rate with computed AQL.

---

## v3.0 — Research-grade candidates

Long-horizon architectural directions. Not feasible as drop-in additions; require infrastructure development.

### v3.0-C1 — Tool receipts (cryptographic execution grounding)

**Status:** RESEARCH
Sidecar process logs every coder tool invocation (file reads, shell commands, network calls) with cryptographic signature outside the agent's control. Receipts cited in reports; coder cannot fabricate. Lightweight alternative to zero-knowledge proofs (reference: arXiv on tool-grounding, 2026).

### v3.0-C2 — Federation across AADP instances

**Status:** RESEARCH
Cross-project pattern catalog. Multiple AADP instances (different teams, different domains) share violation patterns via a federation protocol. Surfaces universal vs. domain-specific failure modes.

### v3.0-C3 — Cryptographic substrate signing

**Status:** RESEARCH
Decision-lock entries cryptographically signed by Vijay's key. Audit trail tamper-evident. Adopters with regulatory requirements can use AADP as the integrity layer.

---

## Cadence

AADP follows evidence-driven cadence, not calendar-driven. Versions ship when criteria are met, not on a schedule. The Release Monitor agent (see v2.0-C4) tracks cycle accumulation and surfaces a recommendation when bump thresholds are crossed.

Realistic cadence based on current evidence rate:

- **v1.1** — likely Q3 2026 (3+ candidates locked from operational evidence)
- **v2.0** — likely Q4 2026 / Q1 2027 (Critic agent or structured substrate validated across 20+ cycles)
- **v3.0** — 2027 or later (research-grade infrastructure dependencies)

These are estimates, not commitments. The protocol writes its own version cadence via accumulated evidence.

---

## How to propose a candidate

Open an issue in this repo with the following structure:

1. **Pattern observed** — what discipline gap or improvement opportunity surfaced
2. **Source** — production cycle or analysis that surfaced it
3. **Proposed amendment** — specific change to §1 / §3 / §4 / §5 / §6
4. **Promotion criterion** — what operational evidence would justify locking

Issues meeting these criteria are reviewed for inclusion as v1.x-Cn or v2.0-Cn candidates.

---

## License

This roadmap, like the protocol itself, is MIT-licensed. Forks and adaptations welcome.

---

*Last updated: 2026-05-15. Maintained by Vijayaprakash Govindarajan.*
