# Resume spacing guide

All adjustable layout values live in:

```text
layout/spacing.tex
```

The main rule is: adjust the most specific variable first.

## Common spacing tasks

| Goal | Adjust this variable |
|---|---|
| Header name row to contact links | `\resumeHeaderNameToLinksSpacing` |
| Header block to first section | `\resumeHeaderAfterSpacing` |
| Section title/rule to first entry | `\resumeSectionAfterSpacing` |
| Education entry to next education entry | `\resumeGapAfterEducationEntryBeforeNextEducationEntry` |
| Degree line to honors/GPA line | `\resumeEducationDetailBeforeSpacing` |
| Honors/GPA line to coursework line | `\resumeEducationDetailBeforeSpacing` and `\resumeEducationDetailAfterSpacing` |
| Role heading to first bullet | `\resumeBulletListTopSep` |
| Bullet to bullet within the same role/project | `\resumeBulletListItemSep` |
| Role bullets to next role under the same company | `\resumeGapAfterRoleBulletListBeforeNextRoleHeading` |
| Company bullets to next company heading | `\resumeGapAfterCompanyBulletListBeforeNextCompanyHeading` |
| Final content of one section to next section heading | `\resumeGapAfterSectionContentBeforeNextSectionHeading` |
| Project bullets to next project heading | `\resumeGapAfterProjectBulletListBeforeNextProjectHeading` |

## Why relationship variables exist

The old spacing model used one broad bullet-list ending variable. That made one setting affect unrelated cases, including:

- a KBR role's final bullet to the next KBR role heading
- the final KBR role to the Harman company heading
- the final Work Experience bullet to the Software Projects section heading
- one project bullet list to the next project heading

Those are different relationships, so they now have different variables.

## Relationship spacing commands

The relationship variables are inserted in the content files through explicit commands.

| Command | Used for | Variable it reads |
|---|---|---|
| `\resumeBetweenEducationEntries` | One school entry to the next school entry | `\resumeGapAfterEducationEntryBeforeNextEducationEntry` |
| `\resumeBetweenSameCompanyRoles` | One role's bullets to the next role under the same company | `\resumeGapAfterRoleBulletListBeforeNextRoleHeading` |
| `\resumeBetweenCompanies` | One company's final role to the next company | `\resumeGapAfterCompanyBulletListBeforeNextCompanyHeading` |
| `\resumeBeforeNextSection` | Previous section content to next section heading | `\resumeGapAfterSectionContentBeforeNextSectionHeading` |
| `\resumeBetweenProjects` | One project's bullets to the next project heading | `\resumeGapAfterProjectBulletListBeforeNextProjectHeading` |

## Examples

To tighten the space between a KBR role's final bullet and the next KBR role heading:

```tex
\setlength{\resumeGapAfterRoleBulletListBeforeNextRoleHeading}{0pt}
```

To loosen the space between Work Experience and Software Projects:

```tex
\setlength{\resumeGapAfterSectionContentBeforeNextSectionHeading}{8pt}
```

To tighten bullet spacing within the same role:

```tex
\setlength{\resumeBulletListItemSep}{1pt}
```

## Component spacing versus relationship spacing

Use **component spacing** when changing spacing inside a repeated object:

- heading to first bullet
- bullet to bullet
- degree line to honors/GPA
- section rule to first entry

Use **relationship spacing** when changing spacing between different objects:

- role to role
- company to company
- section to section
- project to project

## Recommended adjustment process

1. Find the exact visual gap you want to change.
2. Check the table above.
3. Adjust the most specific variable.
4. Recompile in Overleaf.
5. Only adjust a broader variable if multiple related gaps need to change together.
