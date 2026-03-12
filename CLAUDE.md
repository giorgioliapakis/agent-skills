# Agent Skills

## Structure

`skills/` holds each skill in its own folder (kebab-case). Each skill has a `SKILL.md` with YAML frontmatter (`name`, `description`) and Markdown guidance. Some skills include `references/` for progressive disclosure.

## Install

```bash
npx skills add giorgioliapakis/agent-skills
```

## Skill Authoring

### Frontmatter

- `name`: max 64 chars, lowercase letters/numbers/hyphens only
- `description`: max 1024 chars, non-empty, no XML tags

### Description style

- Third-person voice: "Generates images..." not "Use this to generate..."
- Include what the skill does + "Use when..." trigger phrases with specific keywords

### Body rules

- Keep SKILL.md under 500 lines; split into reference files if longer
- References must be one level deep from SKILL.md
- Reference files over 100 lines should start with a table of contents
- Use consistent terminology within a skill

## Maintenance

- When adding or removing a skill, update README.md
- When renaming folders or reference files, grep all SKILL.md files for stale paths
