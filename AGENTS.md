# Repository Guidelines

## Project Structure & Module Organization
This repository is a single-document LaTeX project. [`main.tex`](C:\Users\V10617\OneDrive - UNIPA\materie magistrale\inf theory\latex\main.tex) is the entry point and contains the preamble, theorem environments, custom macros, and the full course text. Store figures in [`images/`](C:\Users\V10617\OneDrive - UNIPA\materie magistrale\inf theory\latex\images). Import figures in LaTeX as vector PDFs through `\includegraphics`; if a figure has an editable source (for example a TikZ/standalone `.tex` file or an original `.svg`), keep that source next to the exported PDF but do not reference the SVG directly from `main.tex`. Generated artifacts such as `main.pdf`, `.aux`, `.log`, `.toc`, `.fls`, and `.fdb_latexmk` are written in the repository root and should never be edited by hand.

## Build, Test, and Development Commands
Use `latexmk` for document builds:

- `latexmk -pdf main.tex`: build the main document.
- `latexmk -pdf -pvc main.tex`: rebuild automatically while editing.
- `latexmk -pdf -cd images/kraft-mcmillan_vector.tex`: rebuild the standalone vector figure PDF after editing its TikZ source and keep its build artifacts inside `images/`.
- `latexmk -c`: remove auxiliary files.
- `latexmk -C`: remove auxiliary files and generated PDFs.

If you edit a standalone figure under `images/`, rebuild that figure first and then rebuild `main.tex`.

## Coding Style & Naming Conventions
Keep source files in UTF-8. Indent nested LaTeX environments consistently with 4 spaces, matching the existing document. Define reusable commands only in the preamble, and keep section content focused on one topic at a time. Use descriptive lowercase labels with stable prefixes such as `eq:...`, `fig:...`, `theorem_...`, and `example_...`. Keep figure filenames descriptive and lowercase.

## Writing & Mathematical Style
The body text is written primarily in Italian, with English technical terms introduced only when they are standard for the topic or useful for comparison. Follow the existing teaching pattern:

- introduce concepts first with prose, then formalize them with `definizione`, `theorem`, displayed equations, or proofs;
- after abstract statements, add intuition, a worked example, or an explanatory paragraph when the argument would otherwise feel too compressed;
- use `\footnote{...}` for clarifications, side explanations, or terminology notes, not for bibliography;
- prefer `itemize` and `enumerate` for assumptions, algorithm steps, case splits, and property lists;
- keep notation stable once introduced and reuse the same symbols across nearby explanations;
- use `\textbf{...}` for terminology and emphasis, and reserve `\uline{...}` for key caveats or contrasts that deserve visual stress.

## Tables, Figures, and References
Tables in `main.tex` are typically centered, use bold header rows, and often rely on `\lbox` to keep short codewords visually aligned. Figures should have Italian captions, descriptive labels, and an explicit discussion in the surrounding prose explaining what the reader should notice. Prefer vector graphics, either as standalone-generated PDFs or directly in LaTeX environments such as `forest`. Use `\eqref{...}` for equations and `\autoref{...}` for figures.

## Testing Guidelines
There is no automated test suite in this repository. Validation means a clean LaTeX build and a quick visual review of [`main.pdf`](C:\Users\V10617\OneDrive - UNIPA\materie magistrale\inf theory\latex\main.pdf). Before submitting changes, run the full build, check for broken references, and confirm that equations, theorem environments, tables, forest diagrams, and imported vector figures render correctly.

## Commit & Pull Request Guidelines
The repository currently has no meaningful shared history, so use clear imperative commit subjects such as `Add Kraft-McMillan figure PDF` or `Fix LaTeX figure import`. Keep subjects under 72 characters. Pull requests should summarize the edited sections, mention any new figure sources or generated PDF assets, and include screenshots only when layout or rendering changes materially.
