# Repository Guidelines

## Project Structure & Module Organization
This repository is a single-document LaTeX project. [`main.tex`](C:\Users\V10617\OneDrive - UNIPA\materie magistrale\inf theory\latex\main.tex) is the entry point and contains the preamble, theorem environments, custom macros, and the full course text. Store figures in [`images/`](C:\Users\V10617\OneDrive - UNIPA\materie magistrale\inf theory\latex\images). Import figures in LaTeX as vector PDFs through `\includegraphics`; if a figure has an editable source (for example a TikZ/standalone `.tex` file or an original `.svg`), keep that source next to the exported PDF but do not reference the SVG directly from `main.tex`.

For diagrams that become visually or logically articulated, prefer moving them into a standalone source under `images/` and including only the generated PDF from `main.tex`. This keeps the main document readable and makes iterative work on figures faster. Generated artifacts such as `main.pdf`, `.aux`, `.log`, `.toc`, `.fls`, and `.fdb_latexmk` are written in the repository root and should never be edited by hand.

The parent course directory [`C:\Users\V10617\OneDrive - UNIPA\materie magistrale\inf theory`](C:\Users\V10617\OneDrive - UNIPA\materie magistrale\inf theory) contains the teaching material for the subject, organized in numbered folders and related archives. Treat that material as a reference source for the project: consult it when the user explicitly asks to align with the slides, when a theorem/definition/order of topics needs to be checked against the course material, or when verifying notation or examples would materially improve accuracy. Do not depend on those files continuously by default, because the notes are meant to be a re-elaboration of the material rather than a direct transcription.

## Build, Test, and Development Commands
Use `latexmk` for document builds:

- `latexmk -pdf main.tex`: build the main document.
- `latexmk -pdf -pvc main.tex`: rebuild automatically while editing.
- `latexmk -pdf -cd images/kraft-mcmillan_vector.tex`: rebuild the standalone vector figure PDF after editing its TikZ source and keep its build artifacts inside `images/`.
- `latexmk -pdf -cd images/albero-ternario.tex`: rebuild the standalone ternary-tree figure after editing its `forest` source.
- `latexmk -c`: remove auxiliary files.
- `latexmk -C`: remove auxiliary files and generated PDFs.

If you edit a standalone figure under `images/`, rebuild that figure first and then rebuild `main.tex`.

## Coding Style & Naming Conventions
Keep source files in UTF-8. Indent nested LaTeX environments consistently with 4 spaces, matching the existing document. Define reusable commands only in the preamble, and keep section content focused on one topic at a time. Use descriptive lowercase labels with stable prefixes such as `eq:...`, `fig:...`, `theorem_...`, and `example_...`. Keep figure filenames descriptive and lowercase.

## Document Organization
Organize the notes by conceptual questions, not by slide boundaries or page count. When the central question changes, open a new `\section`; when you are still answering the same question but moving to a major subtopic, use `\subsection`; when you need a navigable and descriptive item inside the index, use `\subsubsection`.

Follow these structural preferences:

- keep the table of contents descriptive and useful for navigation; the document is configured so `\subsubsection` entries appear in the index, and this should generally be preserved;
- prefer informative titles over generic ones when possible, especially for theorem-heavy or example-heavy parts;
- use `\subsubsection` for substantial examples, algorithms, properties, or exercises when they should be reachable from the table of contents;
- reserve `\paragraph` for short local remarks, tiny examples, or brief observations that do not need their own index entry;
- if a section grows by accretion and starts answering multiple different questions, split it rather than keeping everything under a broad heading such as `Introduzione`;
- when extending the notes, a good high-level progression is: `Introduzione`, `Misura dell'informazione`, `Codifica di sorgente`, `Limiti fondamentali e codici ottimali`.

## Writing & Mathematical Style
The body text is written primarily in Italian, with English technical terms introduced only when they are standard for the topic or useful for comparison. Follow the existing teaching pattern:

- introduce concepts first with prose, then formalize them with `definizione`, `theorem`, displayed equations, or proofs;
- after abstract statements, add intuition, a worked example, or an explanatory paragraph when the argument would otherwise feel too compressed;
- use `\footnote{...}` for clarifications, side explanations, or terminology notes, not for bibliography;
- prefer `itemize` and `enumerate` for assumptions, algorithm steps, case splits, and property lists;
- keep notation stable once introduced and reuse the same symbols across nearby explanations;
- use `\textbf{...}` for terminology and emphasis, and reserve `\uline{...}` for key caveats or contrasts that deserve visual stress.

## Collaboration Preference
Unless the user explicitly asks for a file change, keep the interaction at the level of explanation, feedback, drafting, or proposed text only. In those cases, explain the relevant concept, reasoning, or suggested wording clearly in prose instead of editing files. Apply effective modifications to the repository files only when the user clearly says to do so.

## Tables, Figures, and References
Tables in `main.tex` are typically centered, use bold header rows, and often rely on `\lbox` to keep short codewords visually aligned. Prefer the `table` environment for project consistency, especially when a table has a caption, label, or may need to be referenced. For small local examples that are part of an explanatory passage and must stay exactly in textual order, it is acceptable to center a `tabular` directly with `center` instead of using a floating `table`; use this exception sparingly and only when preserving the flow of the example matters more than table numbering or floating behavior. Figures should have Italian captions, descriptive labels, and an explicit discussion in the surrounding prose explaining what the reader should notice. Prefer vector graphics, either as standalone-generated PDFs or directly in LaTeX environments such as `forest`. For standalone figure sources, comment the main style/configuration blocks so that node styles, edge styles, spacing, and layout choices remain easy to understand and edit later. Use `\eqref{...}` for equations and `\autoref{...}` for figures.

## Testing Guidelines
There is no automated test suite in this repository. Validation means a clean LaTeX build and a quick visual review of [`main.pdf`](C:\Users\V10617\OneDrive - UNIPA\materie magistrale\inf theory\latex\main.pdf). Before submitting changes, run the full build, check for broken references, and confirm that equations, theorem environments, tables, forest diagrams, and imported vector figures render correctly.

## Commit & Pull Request Guidelines
The repository currently has no meaningful shared history, so use clear imperative commit subjects such as `Add Kraft-McMillan figure PDF` or `Fix LaTeX figure import`. Keep subjects under 72 characters. Pull requests should summarize the edited sections, mention any new figure sources or generated PDF assets, and include screenshots only when layout or rendering changes materially.
