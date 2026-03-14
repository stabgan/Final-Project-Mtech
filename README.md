# Hybrid Data Augmentation for Disease Identification from Clinical Notes

> M.Tech thesis — IIT Madras, 2025

Improving rare disease coverage in automated ICD-10 coding by combining LLM-driven synthetic clinical text generation with knowledge-guided validation on the MIMIC-IV dataset.

## Overview

Clinical datasets like MIMIC-IV exhibit a severe long-tail distribution: a handful of ICD codes dominate while thousands of rare codes appear fewer than five times. Standard classifiers learn to predict common codes well but fail on uncommon diagnoses — exactly the ones that matter most for rare disease identification.

This thesis proposes a four-stage pipeline to close that gap:

1. **Synthetic data generation** — Large language models produce factually grounded discharge summaries guided by SNOMED CT and Orphanet ontologies, targeting underrepresented ICD-10 codes
2. **Multi-phase validation** — Rule-based medical plausibility checks, LLM-based fact verification, and ICD feedback loops filter out hallucinated or inconsistent samples
3. **Advanced classification** — Transformer-based architectures (PLM-ICD, ModernBERT) and synonym-aware networks trained on the augmented corpus, with focal loss and tuned decision thresholds
4. **Explainability** — Attention visualization and SHAP attributions provide transparent, clinician-reviewable predictions

## Key Findings

| Metric | Baseline (KNN) | Target |
|--------|----------------|--------|
| Macro-F1 | 0.12 | ≥ 10–15% improvement on rare codes |
| Similarity duplicates (≥90%) | 260 notes identified | Removed before training |
| Near-identical notes (≥97%) | 6 notes | Confirmed by medical expert |

The MIMIC-IV dataset contains 364,627 patients, 331,793 discharge summaries, and 19,440 unique ICD-10 codes — of which 9,217 appear fewer than 5 times.

## 🛠 Tech Stack

| | Tool | Purpose |
|---|---|---|
| 📊 | MIMIC-IV (v2.2+) | De-identified clinical notes and ICD codes |
| 🗄️ | DuckDB | In-memory SQL for fast data exploration |
| 🧠 | PLM-ICD / ModernBERT | Transformer-based multi-label classification |
| 🔬 | SNOMED CT / Orphanet / UMLS | Medical ontologies for knowledge integration |
| 📈 | scikit-learn / TF-IDF | Baseline models (KNN, Logistic Regression, SVM) |
| 🔍 | MinHash + LSH | Near-duplicate detection in clinical notes |
| ⚡ | QLoRA / Gradient Checkpointing | Memory-efficient fine-tuning on moderate GPUs |
| 📝 | LaTeX (IIT Madras template) | Thesis document preparation |
| 🔄 | DVC | Data version control for reproducibility |

## Repository Structure

```
thesis/                  ← Final thesis (IIT Madras dissertation template)
  thesis.tex             ← Main entry point
  .latexmkrc             ← Build config (pdflatex + bibtex + makeglossaries)
  iitmdissertation.cls   ← Document class
  0-prematter/           ← Dedication, certificate, quote
  1-frontmatter/         ← Abstract, acknowledgements, glossary, notation
  2-mainmatter/
    chapters/            ← Introduction → Lit Review → Problem → Methodology
                            → Dataset → Results → Conclusion
    appendices/          ← General notes, additional details
  3-backmatter/          ← Committee, CV
  references/            ← BibTeX bibliography
  images/                ← Logos and signatures
  mimic_plots/           ← 10 dataset analysis plots (age, codes, notes, etc.)
2025/                    ← Report drafts (Jan–Feb 2025)
30 Nov/                  ← November 2024 drafts
7 Dec/                   ← December 2024 draft
old stuff/               ← Early proposals and presentations
```

## Compiling the Thesis

The thesis uses the `iitmdissertation` document class with `latexmk` and `makeglossaries`.

```bash
cd thesis
latexmk -pdf thesis.tex
```

This runs `pdflatex` → `bibtex` → `makeglossaries` automatically via `.latexmkrc`.

**Requirements:** TeX Live or MiKTeX with `latexmk`, `makeglossaries`, and packages: `graphicx`, `amsmath`, `hyperref`, `pgfgantt`, `glossaries`, `float`, `multirow`.

Alternatively, import the `thesis/` folder into [Overleaf](https://www.overleaf.com) — the glossaries setup is Overleaf-compatible.

## ⚠️ Known Issues

1. **Spaces in folder names** — `30 Nov/`, `7 Dec/`, `old stuff/` can cause issues with some build tools and shell scripts
2. **Appendices not included** — `2-mainmatter/appendices/` contains `appn-general-notes.tex` and `appn-more-details.tex` but neither is `\input`'d in `thesis.tex`
3. **Draft folders lack structure** — earlier drafts in `2025/`, `30 Nov/`, `7 Dec/`, and `old stuff/` are loose `.tex` files with no clear versioning
4. **No runnable code** — this repo contains only the thesis document; experiment code (model training, data pipelines) is not included

## Author

**Kaustabh Ganguly** — Department of Chemical Engineering, IIT Madras

Guided by Mr. Samyabrata Chakraborty and Mr. Debopam Nanda (TCS)
