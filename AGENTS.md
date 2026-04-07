# Repository Guidelines

## Project Structure & Module Organization
This repository is a single-document LaTeX project. [`main.tex`](C:\Users\V10617\OneDrive - UNIPA\materie magistrale\inf theory\latex\main.tex) is the entry point and contains the preamble, theorem definitions, macros, and course content. Store figures in [`images/`](C:\Users\V10617\OneDrive - UNIPA\materie magistrale\inf theory\latex\images); the current project uses SVG assets such as `kraft-mcmillan_vector.svg`. Generated artifacts (`main.pdf`, `.aux`, `.log`, `.toc`, `.fls`, `.fdb_latexmk`) are written in the repository root and should never be edited by hand.

## Build, Test, and Development Commands
Use `latexmk` for all local work:

- `latexmk -pdf -shell-escape main.tex`: build the PDF and allow SVG conversion through the `svg` package.
- `latexmk -pdf -pvc -shell-escape main.tex`: rebuild automatically while editing.
- `latexmk -c`: remove auxiliary files.
- `latexmk -C`: remove auxiliary files and `main.pdf`.

If you add or modify SVG figures, make sure Inkscape is available; the current document relies on `shell-escape` for figure export.

## Coding Style & Naming Conventions
Keep source files in UTF-8. Indent nested LaTeX environments consistently with 4 spaces, matching the existing document. Define reusable commands only in the preamble, and keep section content focused on one topic at a time. Use descriptive lowercase labels with stable prefixes, for example `eq:discrete_source`, `theorem_sardinas_patterson`, and `example_sardinas_patterson_not_ud`. Place new figures under `images/` with descriptive lowercase filenames.

## Testing Guidelines
There is no automated test suite in this repository. Validation means a clean LaTeX build and a quick visual review of [`main.pdf`](C:\Users\V10617\OneDrive - UNIPA\materie magistrale\inf theory\latex\main.pdf). Before submitting changes, run the full build, check for broken references, and confirm that equations, theorem environments, and SVG figures render correctly.

## Commit & Pull Request Guidelines
The repository currently has no commit history, so use clear imperative commit subjects such as `Add Kraft-McMillan example` or `Fix entropy notation`. Keep subjects under 72 characters. Pull requests should summarize the edited sections, mention any new assets or TeX package/tool requirements, and include screenshots only when layout or figure rendering changes materially.
