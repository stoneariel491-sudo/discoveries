# Stigmergic-Quorum Admission Control — documentation package

Complete as of 2026-08-12. Six PDF deliverables, English and French, at
three tiers (research paper, practitioner guide, general-public
explainer), plus this index.

## Contents

| File | Tier | Language | Pages |
|---|---|---|---|
| `paper-en.pdf` | Research paper | English | 6 |
| `paper-fr.pdf` | Research paper | French (native, not a translation) | 6 |
| `practitioner-en.pdf` | Practitioner guide | English | 6 |
| `practitioner-fr.pdf` | Practitioner guide | French (native, not a translation) | 6 |
| `general-public-en.pdf` | General-public explainer | English | 2 |
| `general-public-fr.pdf` | General-public explainer | French (native, not a translation) | 2 |

The two papers carry the full formal content: the admission-state,
per-tick-contribution, score-update, and load-adaptive-threshold
definitions (Definitions 1–4); the steady-state-ceiling and
minimum-ticks-to-admission propositions with proofs argued from the
recurrence actually implemented in `admission_control.py`; the
calibration-tension corollary; the adversarial-evaluation table (five
attack scenarios, numbers independently re-executed via `pytest` for
this package, not copied from memory); the 16-query prior-art search;
an honest threats-to-validity section; and a TikZ pipeline diagram (the
French paper's diagram is the same figure, translated, not a separate
drawing). The French paper was written directly in French rather than
translated from the English prose, and checked against common
English-to-French calques (verb government, word order, false cognates
such as "adresser" for "to address a problem").

The practitioner guides carry the applied material the papers
deliberately exclude: an annotated walkthrough of
`src/admission_control.py`, a five-step tuning procedure built around
the calibration-tension corollary, an integration checklist, a
troubleshooting table built from the two real implementation bugs
caught while building and testing the gate, and a procedure for
adapting the gate to a different admission boundary.

The general-public explainers carry no equations and no code; they
build the same two biological analogies (pheromone-trail decay,
quorum sensing) in plain language, report the same real adversarial
numbers, and state the same honest residual (a patient,
identity-diverse attacker is delayed, not fully blocked) without
softening it.

## Verification

- Every PDF above was produced by a real `pdflatex` (MiKTeX 26.2)
  compile, run twice per document to resolve cross-references, with a
  final compile log showing no errors, no overfull boxes, and no
  undefined references (the two general-public documents use no
  cross-references and needed only one pass).
- Two of the adversarial-evaluation table's cited figures were
  independently re-derived by re-running
  `pytest tests/test_admission_control.py -v -s` against the actual
  `moderation-pipeline-prototype` code during this documentation pass
  (not copied from the earlier session's own report): the persistent
  same-cohort-flood steady-state ceiling (0.5, against a threshold of
  4.0) and the persistent cohort-spoofed-flood delay (measured
  admission at tick 4, against the closed-form prediction of
  approximately 4.85 ticks). Both matched the paper's own reported
  numbers exactly. The spray-attack resource-cost reduction (215 → 15
  admissions, 93.0% fewer) and the load-adaptive-threshold ablation
  spread (0 ticks → 13 ticks) were checked the same way and also
  matched.
- `.tex` sources for all six documents are archived in `build/`, so a
  future revision can regenerate rather than rewrite. The six PDFs live
  at the root of this folder, next to this README.

## Scope note

This package documents one of the three candidates that survived the
project's novelty-pipeline step 2 (dual-seam structural coordination
detection and the danger-model trigger are the other two). Per the
project owner's explicit decision, those two remain at their prior
"consigned, not yet formalized" state deliberately — this session's
scope was this candidate only, taken to completion rather than three
candidates advanced partway.
