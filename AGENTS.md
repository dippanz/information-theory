# Repository Guidelines

## Project Shape
This is a single-document LaTeX project.

- `main.tex` is the entry point and contains the preamble, theorem environments, custom macros, and course notes.
- Store figures under `images/`.
- Include figures from `main.tex` as vector PDFs with `\includegraphics`.
- If a figure has an editable source, such as TikZ/standalone `.tex` or an original `.svg`, keep that source next to the exported PDF; do not reference SVG files directly from `main.tex`.
- Generated files such as `main.pdf`, `.aux`, `.log`, `.toc`, `.fls`, and `.fdb_latexmk` must not be edited by hand.

For diagrams that become visually or logically complex, move them into a standalone source under a topic subfolder of `images/`, then include only the generated PDF from `main.tex`.

## Course Material Policy
The parent course directory (`..`) and the course OneDrive folder are reference material, not text to copy.

Use course material when:

- the user explicitly asks to align with slides or teaching material;
- a theorem, definition, notation, example, or topic order needs checking;
- consulting the material would materially improve accuracy.

Do not rely on slides continuously by default: the notes should be a re-elaboration of the material, not a transcription. When material from slides is used, integrate it naturally into the notes. In `main.tex`, avoid phrases such as "from the slides", "as shown in the slides", or similar provenance markers unless the user explicitly asks for source commentary.

When the user asks to consult slides:

- resolve paths relative to the repository root first, then to `..`;
- if not found, check `C:\Users\emanu\OneDrive - UNIPA\materie magistrale\inf theory\`, including numbered subfolders;
- verify files with `Test-Path -LiteralPath` or `Get-Item -LiteralPath`;
- for PDFs, prefer `pdfinfo` and `pdftotext -layout`;
- if tables or diagrams are unclear, render relevant pages with `pdftoppm` and inspect the images;
- keep temporary rendered slide images while the current paragraph/topic is still being developed, then clean them up when no longer useful or when the user asks;
- treat absolute paths from other machines as obsolete.

## Build And Validation
Use `latexmk` for builds.

- `latexmk -pdf main.tex`: build the main document.
- `latexmk -pdf -pvc main.tex`: rebuild automatically while editing.
- `latexmk -c`: remove auxiliary files.
- `latexmk -C`: remove auxiliary files and generated PDFs.

Standalone figure examples:

- `latexmk -pdf -cd images/kraft-mcmillan/kraft-mcmillan_vector.tex`
- `latexmk -pdf -cd images/kraft-mcmillan/albero-ternario.tex`
- `latexmk -pdf -cd images/huffman/huffman-five-symbol-tree.tex`
- `latexmk -pdf -cd images/huffman/huffman-example-tree.tex`

If a standalone figure under `images/` is edited, rebuild that figure first and then rebuild `main.tex`.

There is no automated test suite. Validation means:

- a clean `latexmk -pdf main.tex` build;
- no broken references or important LaTeX warnings;
- a quick visual review of `main.pdf` when layout, tables, diagrams, or figures changed.

## LaTeX Style
Keep source files in UTF-8. Indent nested LaTeX environments with 4 spaces, matching the existing document.

- Define reusable commands only in the preamble.
- Keep section content focused on one topic at a time.
- Use descriptive lowercase labels with stable prefixes such as `eq:...`, `fig:...`, `theorem_...`, and `example_...`.
- Keep figure filenames descriptive and lowercase.

## Document Organization
Organize the notes by conceptual questions, not by slide boundaries or page count.

- Use `\section` when the central question changes.
- Use `\subsection` for a major subtopic under the same question.
- Use `\subsubsection` for substantial examples, algorithms, properties, exercises, or other entries that should appear in the table of contents.
- Use `\paragraph` only for short local remarks or tiny examples that do not need index visibility.
- Prefer informative titles over generic ones.
- Split broad sections when they start answering multiple different questions.
- When extending the notes broadly, a useful progression is `Introduzione`, `Misura dell'informazione`, `Codifica di sorgente`, `Limiti fondamentali e codici ottimali`.

The table of contents should remain useful and descriptive; `\subsubsection` entries are intentionally included.

## Writing And Mathematical Style
The body text is primarily in Italian. Use English technical terms only when standard or useful for comparison.

Follow this teaching pattern:

- introduce concepts in prose before formalizing them;
- then use `definizione`, `theorem`, displayed equations, proofs, examples, or algorithms as appropriate;
- after abstract statements, add intuition or a worked example when the argument would otherwise feel compressed;
- keep notation stable once introduced;
- use `itemize` and `enumerate` for assumptions, algorithm steps, case splits, and property lists;
- use `\footnote{...}` for clarifications, side explanations, or terminology notes, not bibliography;
- use `\textbf{...}` for terminology and emphasis;
- reserve `\uline{...}` for key caveats or contrasts that deserve visual stress.

## Tables, Figures, And References
Tables in `main.tex` usually have centered layout and bold header rows. Prefer the `table` environment when a table has a caption, label, or may be referenced.

Small local examples may use a centered `tabular` directly when preserving exact textual flow matters more than table numbering.

Use `\lbox` when short codewords need to stay visually aligned, following the existing table style.

Figures should have:

- Italian captions;
- descriptive labels;
- an explicit discussion in the surrounding prose explaining what to notice.

Prefer vector graphics, either as standalone-generated PDFs or directly in LaTeX environments such as `forest`. For standalone figure sources, comment the main style/configuration blocks so that node styles, edge styles, spacing, and layout choices remain easy to edit.

Use `\eqref{...}` for equations and `\autoref{...}` for figures.

## Collaboration Preference
Unless the user explicitly asks for file changes, keep the interaction at the level of explanation, feedback, drafting, or proposed text.

When the user clearly asks for modifications, apply them directly and keep the edits scoped to the relevant part of the project.

## Commit And Pull Request Notes
Use clear imperative commit subjects under 72 characters, for example `Add Kraft-McMillan figure PDF` or `Fix LaTeX figure import`.

Pull requests should summarize edited sections, mention new figure sources or generated PDF assets, and include screenshots only when layout or rendering changes materially.
