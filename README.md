# Discoveries

> **En bref (FR)** — Une technique d'ingénierie née de mon prototype de pipeline de modération,
> rédigée à trois niveaux (article, guide de praticien, explication grand public) et en deux
> langues, soit six PDF, avec leurs sources LaTeX.

An engineering technique that came out of my own work, written up the way a small research
result would be: a paper with a formal model and a prior-art section, a practitioner guide, and a
two-page explainer for non-specialists, in **English and French**.

| Technique | Where it comes from | Read |
|---|---|---|
| [**Stigmergic-quorum admission control**](stigmergic-quorum-admission-control/) | The [moderation pipeline prototype](https://github.com/stoneariel491-sudo/moderation-pipeline-prototype): stopping attackers from flooding an expensive review tier. | [paper (EN)](stigmergic-quorum-admission-control/paper-en.pdf) · [article (FR)](stigmergic-quorum-admission-control/paper-fr.pdf) · [guide](stigmergic-quorum-admission-control/practitioner-en.pdf) · [explainer](stigmergic-quorum-admission-control/general-public-en.pdf) |

## The idea in one paragraph

**Stigmergic-quorum admission control.** Disputed cases compete for a costly review tier. Each
case carries a pressure score that decays every tick, like an ant pheromone trail; only
independent sources reinforce it, repeat sources are discounted, and admission requires crossing a
threshold that rises with how full the tier already is, like bacterial quorum sensing. In the
prototype's adversarial tests this blocks single-tick bursts and same-source floods outright and
slows a spoofed flood; a patient attacker with many distinct identities is delayed, not stopped,
and the paper says so.

## Rebuild the PDFs

The folder keeps its LaTeX sources in `build/`. With MiKTeX, from inside the technique's folder:

```bash
pdflatex -interaction=nonstopmode -aux-directory=build build/paper-en.tex   # run twice for cross-references
```

On TeX Live, use `latexmk -pdf -auxdir=build -outdir=. build/paper-en.tex`. Figures are TikZ, so
there are no image assets to fetch.

## Limits

- Novelty is claimed only **relative to the documented prior-art search** in the paper, and only
  for the combination of techniques; the building blocks are established.
- The admission-control numbers come from simulated attacks in the prototype's test suite, not
  from production traffic.
