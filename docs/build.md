# Building and validating the resume

The canonical source is `resume.tex`. It loads
`layout/spacing.tex`, `layout/commands.tex`, and the section files in
`content/`. The output is a standard PDF; the source itself is the
version-controlled artifact.

## Overleaf (primary editing workflow)

Import the repository as an Overleaf project and select:

- **Main file:** `resume.tex`
- **Compiler:** XeLaTeX
- **Main font:** Atkinson Hyperlegible Next

If Overleaf does not have the font, supply licensed font files through
your own Overleaf project setup. Do not commit font binaries to this
repository. Recompile after editing any content or spacing file,
inspect the generated PDF, then export it from Overleaf.

## GitHub Actions (reproducible source and pinned font revision)

The workflow in `.github/workflows/build-resume.yml` performs the following:

1. Checks out the repository without persisting credentials.
2. Downloads the Regular, Bold, Italic, and BoldItalic font faces from a
   pinned commit of the upstream Google Fonts repository over HTTPS.
3. Runs the SHA-pinned `xu-cheng/latex-action` build with
   `latexmk_use_xelatex: true` and the downloaded font files.
4. Renames `resume.pdf` with the `America/Detroit` build date.
5. Uploads the named PDF using a SHA-pinned `actions/upload-artifact`
   action. Nothing is pushed back to `main`.

`push` builds on `main` run when relevant TeX or workflow files change;
pull requests targeting `main` also trigger a build. To find the output,
open the relevant **Build Resume PDF** workflow run in the GitHub Actions
tab and download the artifact named like
`Joshua-Bisdorf_Resume_10-24-2026.pdf`. Actual names reflect the
workflow's local build date; GitHub may place the file in an extracted
artifact directory.

The font URLs are pinned to a source revision, but the TeX build image
may still change when the upstream action/toolchain changes. For stricter
binary reproducibility, also pin the build environment and verify font
hashes. The current workflow guarantees that the selected source
compiled; it does not guarantee byte-identical PDFs across all runs.

## Optional local build

Install XeLaTeX, latexmk, the packages used by `resume.tex`, and
Atkinson Hyperlegible Next with the name recognized by fontspec.
You can then compile from the repository root:

```sh
latexmk -xelatex -interaction=nonstopmode -halt-on-error resume.tex
```

The font must be installed or otherwise discoverable by XeLaTeX.
`fontawesome5`, `fontspec`, `titlesec`, `enumitem`, and the other
required LaTeX packages must also be available. A standard
pdfLaTeX invocation is intentionally rejected by `resume.tex`.

To remove local auxiliary files without removing the PDF:

```sh
latexmk -c resume.tex
```

These local commands are optional; a local LaTeX toolchain is not
required when using Overleaf or the GitHub Actions artifact.

## Review checklist

Before exporting a resume or publishing a PDF:

1. Confirm dates, role names, technology lists, and accomplishments
   against the current source.
2. Confirm the title, contact links, and expected sections are visible.
3. Inspect the PDF at normal zoom for cut-off content, empty pages,
   awkward line wraps, and heading/bullet alignment.
4. Verify the intended page count. A successful TeX compilation alone
   does not enforce a one-page layout.
5. Check the compiler log for overfull `\hbox` or `\vbox` warnings.
6. If space is tight, adjust the most specific value in
   `layout/spacing.tex` rather than inserting raw `\vspace` in bullets.
7. Only after review, export or copy the PDF to its intended publication
   location. The GitHub workflow does not automatically update a
   resume copy hosted in another repository.

## Troubleshooting

**The font cannot be found:** confirm the font family is installed under
the name `Atkinson Hyperlegible Next`. In CI, check the pinned font
download step and the XeLaTeX step.

**The compiler reports an engine error:** select XeLaTeX, not
pdfLaTeX or LuaLaTeX. The source explicitly requires XeLaTeX.

**The PDF overflows a page:** review new bullet lengths, paragraph wraps,
and the spacing variables. Consult [spacing.md](spacing.md).

**The Actions run passed but the website still shows the old resume:**
the workflow only uploads a PDF artifact to GitHub Actions. Update
the external site's hosted PDF separately after visual review.
