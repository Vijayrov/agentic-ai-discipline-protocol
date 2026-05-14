# Agentic AI Discipline Protocol (AADP)

> A formal protocol for deploying AI agents in production with measurable anti-hallucination guardrails.

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Version](https://img.shields.io/badge/version-1.0-blue.svg)](#)
[![Status](https://img.shields.io/badge/status-production--validated-brightgreen.svg)](#)

**Author:** Vijayaprakash Govindarajan
**Locked:** 2026-05-11 · Amended 2026-05-12, 2026-05-13
**Origin:** Extracted from [MAYA](./case-studies/MAYA_anonymized.md), a production multi-agent AI educational system.

---

## What This Is

AADP is a written contract that governs the prompt-and-report cycle between AI agents and a human decision-maker in a production deployment. It formalises four elements:

1. **Role Separation** — distinct authorities for orchestrator agent, executor agent, and human decision-maker
2. **Eleven Anti-Hallucination Invariants** — binding constraints on both AI agents
3. **Substrate Engineering** — versioned context files that preserve discipline across sessions
4. **Failure-Mode Escalation** — observed deviations trigger discipline notes; recurring deviations trigger decision-level locks

The protocol is content-domain agnostic. It was extracted from a curriculum-aligned educational AI project, but applies to any solo or small-team production AI deployment using foundation-model agents.

## Why This Exists

Production AI deployments using foundation models face three persistent risks:

- **Hallucination** — agents invent facts, file paths, or references
- **Scope creep** — agents tidy adjacent work without authorization, often fabricating in the process
- **Context loss** — discipline degrades across sessions as conversation history is truncated

Most existing "responsible AI" frameworks target model training and enterprise policy. AADP targets the **operator level**: how a single architect or small team can deploy AI co-workers reliably, with the rigour Lean Six Sigma applies to manufacturing processes.

The eleven invariants function as poka-yoke devices. The escalation pattern is statistical-process-control logic applied to agent behaviour. The substrate is configuration management. AADP is what happens when you apply 30 years of operations discipline to AI agents.

## The Eleven Invariants

| ID | Invariant | Plain-English Summary |
|----|-----------|------------------------|
| **INV-1** | Every claim is labelled | Each claim carries VERIFIED (disk-cited), INFERRED (rationale-cited), or HYPOTHESIS (test-cited). Unlabelled claims are violations. |
| **INV-2** | File paths verified before cited | Before writing `path/to/file.x`, confirm it exists. Citing a hallucinated path is a violation. |
| **INV-3** | Tool output is quoted, not paraphrased | Show the command and its verbatim output. Summaries lose the evidence. |
| **INV-4** | Banned soft-claim phrasings | "I assume", "it seems", "presumably", "should work", "probably", "likely" — replace with verified evidence or an explicit open question. |
| **INV-5** | Deductive chains are explicit | "Because X is true (verified at &lt;citation&gt;), Y follows." X must be VERIFIED before Y is claimed. |
| **INV-6** | When in doubt, STRATEGIC FLAG | Never guess. Surfacing uncertainty is always the right move. List flag triggers individually, not consolidated. |
| **INV-7** | Scope expansion is a flag, not a feature | If execution uncovers a new problem, stop the affected task, document the discovery, complete the rest of the prompt, exit cleanly. Pattern continuation is not authorization. |
| **INV-8** | Disk reality beats chat memory | If chat history claims X and disk shows ¬X, disk wins. Chat memory is unreliable across sessions and agents. |
| **INV-9** | Re-verify after every change | The test baseline must be re-checked, not assumed, after any code change. |
| **INV-10** | Pre-action read | Coder reads referenced substrate files before any action. Orchestrator reads the handover and any referenced spec before drafting any prompt. No exceptions. |
| **INV-11** | Substrate writes cite verifiable source | Any write to locked-content documents or curriculum-content fields requires source citation per write (not header-only). Pattern-guessing is not a verifiable source. |

Full text and provenance of each invariant lives in [CHAT_CODER_PROTOCOL.md](./CHAT_CODER_PROTOCOL.md).

## How To Use This Protocol

1. **Read** [CHAT_CODER_PROTOCOL.md](./CHAT_CODER_PROTOCOL.md) top-to-bottom before any work.
2. **Adapt** the §1 role definitions to your specific agents (orchestrator, executor, and any specialised sub-agents).
3. **Adapt** the §2 Prompt Contract and §3 Report Contract to your tooling.
4. **Keep** the §4 invariants intact — they are content-domain agnostic and binding.
5. **Set up** a substrate with the four minimum files: `DECISIONS.md`, `SESSION_STATE.md`, `CHANGELOG.md`, and your domain-specific rule file(s). Templates in [substrate-templates/](./substrate-templates/).
6. **Begin** work with the prompt skeleton in [skeletons/PROMPT_SKELETON.md](./skeletons/PROMPT_SKELETON.md).
7. **When deviations occur**, follow the failure-mode escalation pattern in §5: discipline note for first occurrence, decision-level lock on recurrence.

## Repository Structure

```
agentic-ai-discipline-protocol/
├── README.md                         ← you are here
├── LICENSE                           ← MIT
├── CHAT_CODER_PROTOCOL.md            ← the canonical protocol
├── case-studies/
│   └── MAYA_anonymized.md            ← origin case study
├── skeletons/
│   ├── PROMPT_SKELETON.md            ← copy-paste prompt starting point
│   └── REPORT_SKELETON.md            ← copy-paste report starting point
└── substrate-templates/
    ├── DECISIONS.md.template
    ├── SESSION_STATE.md.template
    └── CHANGELOG.md.template
```

## Validation Evidence

AADP v1.0 was validated in production on the MAYA project (multi-agent educational AI deployment, southern India, 2026 pilot). Across one three-day observed window after the discipline lock:

- 27 locked decisions captured
- 23 read-only audit cycles closed
- 30 legacy artefacts safely archived
- 84/84 test floor passing, never regressed
- **Zero** scope-violation recurrences after the discipline lock was applied
- 100% curriculum-alignment backfill across 11 stages

Two prior INV-7 violations (anticipatory write of unverified content; fabricated curriculum chapter names) were detected, surfaced, remediated, and the pattern locked at decision level. The lock then held across all subsequent cycles in the observation window. Details in [case-studies/MAYA_anonymized.md](./case-studies/MAYA_anonymized.md).

## Versioning

- **v1.0** (2026-05-11) — initial lock with 9 invariants
- **v1.1** (2026-05-12) — INV-11 added (substrate source-citation), INV-7 reinforced with pattern-continuation prohibition; failure-escalation pattern formalised
- **v1.2** (2026-05-13) — handover-write workflow clarified; per-write source-citation discipline; STRATEGIC FLAG individual-listing requirement

Versions are tagged. Substantive amendments require a documented decision entry. See [CHAT_CODER_PROTOCOL.md §7](./CHAT_CODER_PROTOCOL.md#7--maintenance).

## Citation

If you use this protocol or build on it, please cite:

> Govindarajan, V. (2026). *Agentic AI Discipline Protocol (AADP) v1.0*. GitHub.

BibTeX:

```bibtex
@misc{govindarajan2026aadp,
  author = {Govindarajan, Vijayaprakash},
  title  = {Agentic AI Discipline Protocol (AADP) v1.0},
  year   = {2026},
  url    = {https://github.com/vijayaprakash-govindarajan/agentic-ai-discipline-protocol}
}
```

## License

MIT License. See [LICENSE](./LICENSE).

The protocol document, prompt/report skeletons, and substrate templates are open-source. The MAYA product from which the protocol was extracted remains proprietary and is not included in this release.

## Contributing

Contributions welcome. Before opening a pull request:

- Open an issue first for any substantive change to the invariants or contract structures
- Preserve INV-1 through INV-11 in spirit if not literal letter
- Add newly observed failure modes with a citation to the report or transcript in which the deviation occurred

## Related Work

AADP is complementary to, not a replacement for:

- **Constitutional AI** (Bai et al., Anthropic, 2022) — model-training-time alignment
- **CRISP-DM / PMI-CPMAI** — data-science project lifecycle methodology
- **Agile / Scrum** — team coordination patterns
- **Lean Six Sigma** — the discipline lineage AADP draws from

AADP operates at a different layer: the runtime contract between an architect and AI agents in production.

## About The Author

Vijayaprakash Govindarajan is an Operations and AI Systems professional based in Coimbatore, India. 30+ years of field experience across offshore operations (Saipem, Ventura), R&D operations management (PSG-COE), and independent consulting. Credentials: PMP, CSM, Lean Six Sigma Black Belt (CSSC), Executive Certificate in Lean Operations Management & Six Sigma from IIM Visakhapatnam (Reg No: IIMV50U24LOMB2-058), Google Data Analytics Professional Certificate, Google AI Essentials, PMI GenAI for PMs, and a stack of 40+ project, agile, and AI certifications. Architect of MAYA.

**Contact**
- LinkedIn: [linkedin.com/in/vijayaprakash-govindarajan](https://www.linkedin.com/in/vijayaprakash-govindarajan/)
- Email: vijayrov@gmail.com

---

*If AADP saves you from one production hallucination, it has paid for itself. If you adopt it and have feedback, open an issue — observed failure modes are how this protocol got built.*
