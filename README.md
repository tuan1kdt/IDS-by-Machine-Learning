# AI-Powered Intrusion Detection System — Final Report

LaTeX source for the final report of the **Information Security** course at
Ton Duc Thang University (TDTU).

**Topic.** An AI-Powered Intrusion Detection System: Real-Time Detection of
Network Attacks using Machine Learning on the CIC-IDS2017 Dataset.

**Authors.**

| Name                   | Student ID |
| ---------------------- | ---------- |
| Le Anh Tuan            | 252805005  |
| To Hoang Dao           | 252805401  |
| Nguyen Tu Thanh Duy    | 252805701  |

The document follows the Springer **LNCS** (Lecture Notes in Computer Science)
format via `llncs.cls` and the `splncs04` bibliography style, both shipped
inside this folder.

---

## Quick start

```bash
make              # build main.pdf (two pdflatex passes, resolves all refs)
make view         # open the compiled PDF
make clean        # remove LaTeX aux files
make distclean    # clean + remove main.pdf
make help         # list all targets
```

A successful build produces `main.pdf` in this directory.

---

## Prerequisites

A working **TeX Live** (or MacTeX / MiKTeX) installation with the following
collections:

| Collection                       | Provides                                      |
| -------------------------------- | --------------------------------------------- |
| `texlive-latex-base`             | core `pdflatex`, `\documentclass`             |
| `texlive-latex-recommended`      | `hyperref`, `booktabs`, `enumitem`, `xcolor`  |
| `texlive-latex-extra`            | `multirow`, `float`                           |
| `texlive-fonts-recommended`      | CM / EC fonts                                 |
| `texlive-pictures`               | `tikz`, `pgfplots`                            |
| `texlive-science`                | `algorithm`, `algpseudocode` (a.k.a. `collection-mathscience` via `tlmgr`) |

### Install on Ubuntu / Debian

```bash
sudo apt-get install -y \
    texlive-latex-base texlive-latex-recommended texlive-latex-extra \
    texlive-fonts-recommended texlive-pictures texlive-science
```

### Install on macOS (Homebrew + MacTeX)

```bash
brew install --cask mactex-no-gui
# then, if algorithm.sty is missing, pull it via tlmgr:
sudo tlmgr update --self
sudo tlmgr install collection-mathscience
```

### Install on Windows

Install **MiKTeX** (https://miktex.org) and enable "install missing packages
on the fly." Alternatively install TeX Live with `collection-mathscience`
selected.

---

## Project layout

```
report/
├── Makefile              # build recipes (this folder's entry point)
├── README.md             # you are here
├── main.tex              # title, author block, abstract, \input for sections, bibliography
├── llncs.cls             # Springer LNCS class (vendored)
├── splncs04.bst          # Springer LNCS bib style (vendored)
│
├── 1/                    # Section 1 — Introduction
│   └── 1.tex
│
├── 2/                    # Section 2 — Background and Foundations
│   ├── 2.tex             # section parent (\input 2.1-2.4)
│   ├── 2.1.tex           # Network Traffic and Attack Taxonomy
│   ├── 2.2.tex           # The CIC-IDS2017 Dataset
│   ├── 2.3.tex           # Data Preprocessing
│   └── 2.4.tex           # Machine Learning Foundations
│
├── 3/                    # Section 3 — Proposed System: An ML-Based IDS Pipeline
│   ├── 3.tex             # section parent (\input 3.1-3.6)
│   ├── 3.1.tex           # Problem Statement
│   ├── 3.2.tex           # System Architecture Overview (TikZ pipeline diagram)
│   ├── 3.3.tex           # Feature Engineering
│   ├── 3.4.tex           # Model Design (RF / XGBoost / DNN)
│   ├── 3.5.tex           # Training Procedure (Algorithm 1 pseudocode)
│   └── 3.6.tex           # Real-Time Inference Engine (Algorithm 2 pseudocode)
│
└── 4/                    # Section 4 — Experiments and Results (skeletons only)
    ├── 4.tex             # section parent (\input 4.1-4.7)
    ├── 4.1.tex           # Experimental Setup               [TODO]
    ├── 4.2.tex           # Baselines and Metrics            [TODO]
    ├── 4.3.tex           # Overall Detection Performance    [TODO]
    ├── 4.4.tex           # Per-Class Breakdown              [TODO]
    ├── 4.5.tex           # Ablation Studies                 [TODO]
    ├── 4.6.tex           # Latency and Throughput           [TODO]
    └── 4.7.tex           # Simulated Attack Scenarios       [TODO]
```

Sections 5 (Discussion) and 6 (Conclusion) are not yet present; their
`\input` lines are commented out at the bottom of `main.tex`.

---

## Editing workflow

1. Edit the relevant `<section>/<subsection>.tex` file.
2. Run `make` in this folder.
3. Inspect `main.pdf`.
4. Commit your changes.

Each subsection is an isolated file so multiple authors can work in parallel
without merge conflicts on `main.tex`.

### Conventions

- **English only** for all `.tex` content (course requirement).
- **Labels** follow the pattern `sec:<slug>` (e.g., `sec:feat-eng`,
  `sec:exp-latency`) so forward references remain readable.
- **Bibliography** entries live at the bottom of `main.tex` inside
  `\begin{thebibliography}...\end{thebibliography}`; cite with
  `\cite{ref_xxx}`.
- **Figures** use `tikz` where possible (vector output, no external assets);
  tables use `booktabs` rules (`\toprule`, `\midrule`, `\bottomrule`).
- **Algorithms** use `algorithm` + `algpseudocode` (see Sections 3.5 and 3.6
  for the in-use pattern).

---

## Troubleshooting

**`algorithm.sty not found` / `algpseudocode.sty not found`.**
Install `texlive-science` (Ubuntu/Debian) or
`sudo tlmgr install collection-mathscience` (MacTeX / TeX Live).

**References show as `??`.**
You ran `pdflatex` only once. Run `make` (which runs it twice) or re-run
`pdflatex main.tex` a second time so that `.aux` references resolve.

**`main.aux` error after switching LaTeX engines or class files.**
Run `make clean` to remove stale auxiliary files, then `make` again.

**Overfull / underfull `\hbox` warnings.**
Cosmetic only — these do not block the build. Ignore unless a visually
broken line bothers you; LLNCS's narrow text block produces a few of these
by default in dense technical prose.
