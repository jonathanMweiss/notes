# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a LaTeX-based academic notes document ("Notes From a Student") covering mathematics and computer science topics, with a focus on cryptography, distributed algorithms, and their mathematical foundations.

## Building

The project uses `latexmk` with `biber` for bibliography:

```bash
latexmk -pdf notes-from-a-student.tex
```

Or with plain `pdflatex` (two passes needed for references):

```bash
pdflatex notes-from-a-student.tex && biber notes-from-a-student && pdflatex notes-from-a-student.tex
```

## Document Structure

The main entry point is `notes-from-a-student.tex`. It directly inputs `mathematics/Algebraic-structures.tex` and delegates the rest to `computer-sceince/computer-sceince.tex`.

The preamble requires these packages (all must be present):
- `biblatex` + `\addbibresource{bib.bib}` — bibliography (do **not** also add `\bibliography{}`, which conflicts)
- `listings` — for `lstlisting` code blocks
- `[tikz]{bclogo}` — for info/attention boxes (the `[tikz]` option is required with `pdflatex`; the default PSTricks driver does not work)
- `bbm` — for `\mathbbm{1}` (the `\one` macro)
- A `\newcommand{\todo}` definition
- `definition` and `proposition` theorem environments (in addition to `defn`)

### Content organization

```
mathematics/
  Algebraic-structures.tex   — groups, rings, fields (foundation for crypto)
  probability.tex
  lattice.tex                — stub; lattice content currently lives inline in math.tex

computer-sceince/            (note: typo in directory name, kept for consistency)
  algorithms.tex             — finite fields, GCD, extended Euclidean algorithm
  cryptography.tex           — perfect security, OTP, DH, secret sharing
  cryptography/ECC.tex       — elliptic curve cryptography
  cryptography/homomorphic.tex
  distributed-algorithms.tex — network models, consensus, BFT
  code-theory/main.tex
  quantum/main.tex
```

### Known open issues in the source

- `computer-sceince/computer-sceince.tex` has a `\todo{add order...}` at the top about part organization.
- `mathematics/math.tex` has lattice content written directly in the file rather than inside `mathematics/lattice.tex` (which is empty).
- Grammarly is configured for LaTeX files via `.vscode/settings.json`.
