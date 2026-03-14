# Hybrid Data Augmentation for Disease Identification from Clinical Notes

MTech thesis (IIT Madras, 2025) on improving rare disease coverage in automated ICD coding using synthetic clinical text generation and knowledge-guided validation.

## About

This thesis tackles the long-tail problem in ICD code prediction — rare diseases are underrepresented in real-world clinical datasets like MIMIC, leading to poor model performance on uncommon codes. The approach combines:

- **Synthetic data generation** — LLMs produce factually grounded discharge summaries guided by SNOMED CT and Orphanet ontologies
- **Multi-phase validation** — rule-based medical plausibility checks, LLM-based fact verification, and ICD feedback loops filter out inaccurate samples
- **Efficient training** — QLoRA quantization, gradient checkpointing, and knowledge distillation enable fine-tuning on moderate GPU hardware
- **Explainability** — attention visualization and SHAP attributions for transparent predictions

Models evaluated include transformer-based architectures (PLM-ICD) and synonym-aware networks, with focus on macro-F1 and recall for rare codes.

## Repository Structure

```
thesis/              ← Final thesis (IIT Madras dissertation template)
  thesis.tex         ← Main entry point
  0-prematter/       ← Dedication, certificate, quote
  1-frontmatter/     ← Abstract, acknowledgements, glossary, notation
  2-mainmatter/      ← Chapters (intro → lit review → problem → methodology → dataset → results → conclusion)
  3-backmatter/      ← Committee, CV
  references/        ← BibTeX bibliography
  images/            ← Logos and signatures
  mimic_plots/       ← Dataset analysis plots
2025/                ← Earlier report drafts (v2, v3)
30 Nov/              ← November 2024 drafts
7 Dec/               ← December 2024 draft
old stuff/           ← Early proposals and presentations
```

## Compiling

The thesis uses the `iitmdissertation` document class with `latexmk` and `makeglossaries`.

```bash
cd thesis
latexmk -pdf thesis.tex
```

This runs `pdflatex` + `bibtex` + `makeglossaries` automatically (configured in `.latexmkrc`).

**Requirements:** A full TeX Live or MiKTeX installation with `latexmk`, `makeglossaries`, and standard packages (`graphicx`, `amsmath`, `hyperref`, `pgfgantt`, `glossaries`, `float`, `multirow`).

Alternatively, import the `thesis/` folder into [Overleaf](https://www.overleaf.com) — the glossaries setup is Overleaf-compatible.

## Known Issues

1. **No `.gitignore`** — LaTeX build artifacts (`.aux`, `.log`, `.bbl`, `.blg`, `.glo`, `.gls`, `.toc`, `.lof`, `.lot`, `.out`, `.fls`, `.fdb_latexmk`, `.synctex.gz`) will pollute the repo if compiled locally
2. **Spaces in folder names** — `30 Nov/`, `7 Dec/`, `old stuff/` can cause issues with some build tools and scripts
3. **Appendices not included** — `2-mainmatter/appendices/` contains `appn-general-notes.tex` and `appn-more-details.tex` but neither is `\input` in `thesis.tex`
4. **Draft folders lack structure** — earlier drafts in `2025/`, `30 Nov/`, `7 Dec/`, and `old stuff/` are loose files with no clear versioning

## Author

**Kaustabh Ganguly** — Department of Chemical Engineering, IIT Madras

Guided by Mr. Samyabrata Chakraborty and Mr. Debopam Nanda (TCS)

## License

No license specified.
