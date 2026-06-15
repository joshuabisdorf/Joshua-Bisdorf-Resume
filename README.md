# Resume

LaTeX resume source designed for Overleaf.

## Development workflow

1. Open the project in Overleaf.
2. Set `resume.tex` as the main file.
3. Set the compiler to **XeLaTeX**.
4. Edit resume content in `content/`.
5. Edit layout and spacing values in `layout/`.

The source intentionally does not include a Makefile or local build workflow because Overleaf is the primary development environment.

## Repository structure

```text
resume.tex              Main LaTeX entry point
layout/spacing.tex      Centralized adjustable layout and spacing values
layout/commands.tex     Resume rendering commands and spacing helper commands
content/heading.tex     Name, location, and contact links
content/education.tex   Education section
content/experience.tex  Work Experience section
content/projects.tex    Software Projects section
docs/spacing.md         Spacing variable guide
```

## Editing content

Most resume text changes should happen in `content/`:

- `content/heading.tex` for name, location, and links.
- `content/education.tex` for schools, degrees, honors, GPA, and coursework.
- `content/experience.tex` for work history and bullets.
- `content/projects.tex` for project entries and bullets.

## Editing spacing

All adjustable spacing values are kept in:

```text
layout/spacing.tex
```

The spacing model separates **component spacing** from **relationship spacing**.

Component spacing controls the inside of a repeated component, such as the gap between a heading and its bullets.

Relationship spacing controls the gap between two different resume objects, such as one role's final bullet and the next role heading.

For common spacing tasks, see:

```text
docs/spacing.md
```

## Overleaf notes

- Use **XeLaTeX**. The resume intentionally raises an error if compiled with another compiler.
- The main font is `Atkinson Hyperlegible Next`.
- The final PDF can be exported from Overleaf.
