# Joshua Bisdorf — Resume

The source for a typeset, single-column resume maintained in **LaTeX**. The
document is edited primarily in Overleaf, and GitHub Actions compiles the
same source with **XeLaTeX** to produce a downloadable PDF artifact.

The generated PDF is not committed to this repository. Edit the `.tex`
source files and use Overleaf or the build workflow to obtain a new PDF.

## Quick start (Overleaf)

1. Import the repository into an Overleaf project.
2. Select `resume.tex` as the main document.
3. Select **XeLaTeX** as the compiler; the source rejects other engines.
4. Make the **Atkinson Hyperlegible Next** font available to the Overleaf
   project if it is not already installed.
5. Edit entries in `content/`, recompile, and inspect the PDF before export.

The font is a build dependency. GitHub Actions downloads four font faces
from a pinned upstream revision; the font files are not stored in this
repository. See [the build guide](docs/build.md) for CI and local workflows.

## Repository layout

| Path | Responsibility |
| --- | --- |
| `resume.tex` | XeLaTeX entry point, packages, page geometry, and section formatting |
| `content/heading.tex` | Name, location, and contact links |
| `content/education.tex` | Degrees, dates, and honors |
| `content/experience.tex` | Employment history, role technologies, and bullet points |
| `content/projects.tex` | Selected project headings and descriptions |
| `layout/commands.tex` | Reusable LaTeX resume macros and list delimiters |
| `layout/spacing.tex` | Centralized length registers and spacing values |
| `docs/spacing.md` | Guide to tuning each type of gap |
| `docs/build.md` | Overleaf, CI, font, and PDF artifact instructions |
| `.github/workflows/build-resume.yml` | GitHub Actions PDF build and artifact upload |

The main document inputs the spacing settings first, then the reusable
macros and content files. Keep content in `content/`; avoid embedding
individual jobs or projects in `resume.tex`.

## Editing the resume

The content files use a small set of macros. For example:

```tex
\resumeSubheading
{Company}{Location}
{Role \textnormal{$|$ \emph{C++, CUDA, MATLAB, Python}}}{January 2026 -- Present}
\resumeItemListStart
    \resumeItem{Concise, verifiable accomplishment or responsibility}
\resumeItemListEnd
```

Use `\resumeBetweenSameCompanyRoles`,
`\resumeBetweenCompanies`, and `\resumeBetweenProjects` at the
corresponding boundaries. Each macro's arguments and environment
requirements are described directly above its definition in
`layout/commands.tex`.

**Keep professional claims factual.** Dates, qualifications, role
technologies, and accomplishments should reflect actual work. The current
KBR Software Engineer technology list includes CUDA; the existing bullets
are unchanged.

Special characters in LaTeX text require escaping when applicable:
`\&`, `\%`, `\_`, and `\#`. Prefer the established macros and
avoid manually inserting layout spaces inside content bullets.

## Adjusting typography and spacing

All adjustable layout lengths are defined in `layout/spacing.tex`.
Change the most specific length first:

- **Component spacing:** within a heading, bullet list, or education entry.
- **Relationship spacing:** between roles, companies, projects, or sections.

See [the spacing guide](docs/spacing.md) before altering the layout macros.
After any typography or content change, inspect page count, margins,
overfull-box warnings, and visual alignment in the generated PDF.

## Automated PDF build

The `Build Resume PDF` workflow runs on pull requests targeting `main`
and on `main` pushes that change LaTeX source or the workflow itself.
It checks out source, downloads pinned font files, compiles the resume
with XeLaTeX, and uploads a PDF artifact.

The generated file is named:

```text
Joshua-Bisdorf_Resume_MM-DD-YYYY.pdf
```

The date is evaluated in `America/Detroit` during the workflow run.
Download the artifact from **GitHub → Actions → Build Resume PDF → run
→ Artifacts**. A green build confirms compilation and artifact upload;
review the actual PDF layout before publishing or sending it.

For local compilation prerequisites, build diagnostics, and how to use the
artifact, see [docs/build.md](docs/build.md).

## Documentation convention

Use ordinary LaTeX `%` comments for document and macro documentation.
Describe non-obvious argument order, environment preconditions, and
spacing effects immediately above the relevant macro. This repository
does not use custom RMEIO blocks or a generated API documentation
framework; its TeX macro interface is documented inline.

GitHub Actions and Dependabot configuration use brief YAML comments
that explain purpose and externally relevant behavior.

## Distribution

The compiled resume contains professional and contact information
intended for publication. Review the contents before distributing it.
Other repositories or websites that host an exported PDF are **not**
updated automatically by this repository's Actions workflow; copy a
reviewed PDF to those destinations separately.
