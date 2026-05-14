# Case Study: MAYA — Production Multi-Agent AI System

*An anonymised case study in agentic AI deployment with formal anti-hallucination guardrails.*

**Architect:** Vijayaprakash Govindarajan
**Status:** Production pilot, southern India, May 2026

---

## The Problem

Foundation-model-based AI assistants are increasingly used to build curriculum content at scale, but production deployments face three persistent risks that compound over time:

- **Hallucination** — agents invent facts, file paths, or curriculum references
- **Scope creep** — agents tidy adjacent work without authorization, fabricating content along the way
- **Context loss** — discipline degrades across sessions as conversation history is truncated

These risks are amplified in regulated content domains like school education, where a single fabricated chapter reference can compromise pedagogical integrity and stakeholder trust.

## The Project

**MAYA** is a curriculum-aligned, multilingual numeracy learning system for early-primary children (ages 5–7) in India. Architecture:

- 99 structured lessons across **11 developmental stages** (3 skills per stage × 3 lessons per skill)
- **Multilingual content pipeline** — English source with dedicated translator agents for Hindi and Tamil
- **Flutter mobile delivery layer** running on entry-level Android tablets
- An **84-test "classroom floor"** verifying lesson integrity, re-checked after every change
- **NCERT-aligned content** mapped to the national early-primary mathematics curriculum
- **Production pilot** scheduled at a primary school in southern India

The system was designed and is being delivered by a **single architect coordinating two AI agents** (an orchestration layer and an execution layer) under a formal protocol.

## The Novel Contribution: The Agentic AI Discipline Protocol (AADP)

The core innovation is not the product but the methodology used to build it reliably with AI co-workers. AADP formalises four elements:

1. **Role Separation** — three roles with distinct authorities (orchestrator, executor, human decision-maker)
2. **Eleven Anti-Hallucination Invariants** — binding constraints on both AI agents
3. **Substrate Engineering** — versioned context files preserving discipline across sessions
4. **Failure-Mode Escalation** — observed deviations trigger discipline notes; recurring deviations trigger decision-level locks

See [CHAT_CODER_PROTOCOL.md](../CHAT_CODER_PROTOCOL.md) for the full protocol.

## Measured Results

Across a single three-day observed window under the locked protocol:

| Metric | Result |
|---|---|
| Locked decisions captured | 27 |
| Audits closed (read-only verification cycles) | 23 |
| Legacy artefacts safely archived | 30 |
| Test floor (classroom integrity tests passing) | 84 / 84, never regressed |
| Scope-violation recurrences after discipline lock | **0** |
| Curriculum alignment backfill | 100% of 11 stages, ≈36 lesson entries |

The discipline lock had previously caught two scope-expansion incidents (one anticipatory write of unverified content, one fabricated chapter-name pair). Both were detected, remediated, and the underlying pattern locked at decision level. The lock then ran clean across all subsequent cycles in the observation window.

## Why This Matters

Most published frameworks for "responsible AI" target model training and corporate policy. AADP addresses a different problem: **how a single architect can deploy AI co-workers in production with the rigour Lean Six Sigma applies to manufacturing**.

The 11 invariants are functionally poka-yoke devices. The escalation pattern (note → decision lock) is statistical-process-control logic applied to agent behaviour. The substrate is configuration management. The verbatim-quoting rule is a measurement-system-analysis guardrail. The methodology is content-domain agnostic — extracted here from a curriculum-aligned educational AI project, but applicable to any solo or small-team production AI deployment.

## Release Posture

- **AADP v1.0** is open-sourced under MIT in this repository. The protocol document, prompt/report skeletons, and substrate templates are publicly available.
- **MAYA itself** — the curriculum content, lesson JSONs, translator agents, recording packs, glossary, Flutter app, and pilot deployment artefacts — remains proprietary.
- The split is deliberate: the **methodology** benefits the field; the **product** funds the architect.

## About the Architect

Vijayaprakash Govindarajan, M.Sc. (Electronics), is a Coimbatore-based Operations and AI Systems professional with 30+ years of field experience spanning offshore drilling operations (10+ years with Saipem across Cuba, West Africa, and Kazakhstan), R&D operations management (PSG-COE, Coimbatore), and independent consulting since January 2025.

Credentials include PMP, CSM, Lean Six Sigma Black Belt (CSSC), Executive Certificate in Lean Operations Management & Six Sigma from IIM Visakhapatnam (Aug 2024–Feb 2025, Reg No: IIMV50U24LOMB2-058), Google Data Analytics Professional Certificate, Google AI Essentials, PMI's GenAI for Project Managers credentials, and 40+ certifications across PM, Agile, Lean, and AI completed during 2023–2025.

MAYA represents his synthesis of three decades of operations discipline with applied AI architecture.

## Contact

- **LinkedIn:** https://www.linkedin.com/in/vijayaprakash-govindarajan/
- **Email:** vijayrov@gmail.com

---

*This case study is published with all client, school, and proprietary product details anonymised. The protocol methodology (AADP) is open-sourced under MIT. The MAYA product remains under active development and is not in scope for this release.*
