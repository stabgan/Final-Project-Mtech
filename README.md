<p align="center">
  <img src="thesis/images/iitm-logo.png" alt="IIT Madras Logo" width="120"/>
</p>

<h1 align="center">Hybrid Data Augmentation for Disease Identification from Clinical Notes</h1>

<p align="center">
  <strong>MTech Thesis — Indian Institute of Technology Madras, 2025</strong><br/>
  Department of Chemical Engineering
</p>

<p align="center">
  <img src="https://img.shields.io/badge/degree-M.Tech-blue?style=flat-square" alt="Degree"/>
  <img src="https://img.shields.io/badge/year-2025-green?style=flat-square" alt="Year"/>
  <img src="https://img.shields.io/badge/LaTeX-pdflatex-orange?style=flat-square&logo=latex&logoColor=white" alt="LaTeX"/>
  <img src="https://img.shields.io/badge/template-IIT%20Madras%20Dissertation-critical?style=flat-square" alt="Template"/>
</p>

---

## 📖 About

This thesis tackles the **long-tail problem in automated ICD code prediction** — rare diseases are severely underrepresented in real-world clinical datasets like MIMIC-IV, leading to poor model performance on uncommon diagnostic codes.

The proposed framework combines **LLM-driven synthetic clinical text generation**, **ontology-guided validation**, and **memory-efficient training** to significantly improve recall and macro-F1 for rare ICD codes while maintaining strong performance on common ones.

### Core Contributions

- **Synthetic data generation** — Large language models produce factually grounded discharge summaries guided by SNOMED CT and Orphanet ontologies
- **Multi-phase validation pipeline** — Rule-based medical plausibility checks, LLM-based fact verification, and ICD feedback loops filter out inaccurate samples
- **Efficient training under hardware constraints** — QLoRA quantization, gradient checkpointing, and knowledge distillation enable fine-tuning on moderate GPU setups (6 GB VRAM / Colab Pro+)
- **Explainability & bias analysis** — Attention visualization, SHAP attributions, and integrated gradients for transparent, trustworthy predictions

Models evaluated include transformer-based architectures (PLM-ICD, ModernBERT, MSMN), CNN/RNN baselines (CAML, LAAT), and synonym-aware / hyperbolic-embedding approaches, with focus on rare-code recall.

---

## 🏗️ Repository Structure

```
thesis/                        ← Final thesis (IIT Madras dissertation template)
├── thesis.tex                 ← Main entry point
├── iitmdissertation.cls       ← Custom document class
├── iitmdissertation.sty       ← Companion style package
├── iitm.bst                   ← Bibliography style
├── .latexmkrc                 ← latexmk build configuration
├── 0-prematter/               ← Dedication, certificate, quote
├── 1-frontmatter/             ← Abstract, acknowledgements, glossary, notation
├── 2-mainmatter/
│   ├── chapters/              ← Introduction → Lit Review → Problem Def → Methodology
│   │                            → Dataset Understanding → Results → Conclusion
│   └── appendices/            ← Supplementary notes
├── 3-backmatter/              ← Committee, CV
├── references/                ← BibTeX bibliography
├── images/                    ← Logos & signatures
├── mimic_plots/               ← Dataset analysis plots
└── zz-imp/                    ← Cover & certificate internals

2025/                          ← Earlier report drafts (IIT template v3, report v2)
30 Nov/                        ← November 2024 drafts
7 Dec/                         ← December 2024 draft
old stuff/                     ← Early proposals, presentations, architecture diagrams
```

---

## 🔧 How to Compile

The thesis uses the `iitmdissertation` document class and is built with **pdflatex** via `latexmk`.

### Using latexmk (recommended)

```bash
cd thesis
latexmk -pdf thesis.tex
```

This automatically runs the full `pdflatex → bibtex → makeglossaries → pdflatex` cycle as configured in `.latexmkrc`.

### Manual compilation

```bash
cd thesis
pdflatex thesis.tex
bibtex thesis
makeglossaries thesis
pdflatex thesis.tex
pdflatex thesis.tex
```

### Using XeLaTeX

The class supports XeLaTeX via the `devx` option (uses `fontspec` + `unicode-math` with TeX Gyre Termes). Change the documentclass option in `thesis.tex`:

```latex
\documentclass[mtech, devx, 12pt, a4paper]{iitmdissertation}
```

Then compile with:

```bash
latexmk -xelatex thesis.tex
```

### Using Overleaf

Import the `thesis/` folder into [Overleaf](https://www.overleaf.com) — the glossaries setup is Overleaf-compatible out of the box.

---

## 🛠️ Tech Stack

| Component | Technology |
|-----------|-----------|
| 📝 Typesetting | LaTeX (pdflatex / XeLaTeX) |
| 📦 Document class | Custom `iitmdissertation` (KOMA-Script `scrbook`) |
| 📐 Page layout | `geometry`, `scrlayer-scrpage` |
| 🔤 Typography | `microtype`, `newtxtext`, `newtxmath`, `setspace` |
| 📊 Math | `amsmath`, `amssymb`, `amsthm`, `mathtools` |
| 📚 Bibliography | `natbib` (author-year) + custom `iitm.bst` |
| 📖 Glossary & Notation | `glossaries`, `nomencl` |
| 🖼️ Figures & Tables | `graphicx`, `subcaption`, `booktabs`, `multirow`, `float` |
| 📅 Gantt Charts | `pgfgantt` |
| 🔗 Hyperlinks | `hyperref` |
| 🏗️ Build system | `latexmk` with custom `.latexmkrc` |

---

## ⚠️ Known Issues

1. **No `.gitignore` for LaTeX artifacts** — Compiling locally will generate `.aux`, `.log`, `.bbl`, `.blg`, `.glo`, `.gls`, `.toc`, `.lof`, `.lot`, `.out`, `.fls`, `.fdb_latexmk`, `.synctex.gz` files that pollute the repository
2. **Spaces in folder names** — Directories like `30 Nov/`, `7 Dec/`, and `old stuff/` can cause issues with some build tools, shell scripts, and CI pipelines
3. **Appendices not wired up** — `2-mainmatter/appendices/` contains `appn-general-notes.tex` and `appn-more-details.tex`, but neither is `\input`'d in `thesis.tex`
4. **Duplicate sections in introduction** — `chap-introduction.tex` contains repeated Background, Importance, Challenges, and Problem Statement sections (likely from merging drafts)
5. **Draft folders lack versioning** — Earlier drafts in `2025/`, `30 Nov/`, `7 Dec/`, and `old stuff/` are loose files with no clear version history

---

## 👤 Author

**Kaustabh Ganguly**
Department of Chemical Engineering, IIT Madras

**Guided by:**
- Mr. Samyabrata Chakraborty — Lead Solution Architect & Head of Centre of Excellence, TCS
- Mr. Debopam Nanda — Lead Data Scientist, TCS

---

## 📄 License

No license specified.
