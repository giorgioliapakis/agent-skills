# Agent Skills

Reusable agent skills for Claude Code and other AI coding agents.

## Quick Start

```bash
npx skills add giorgioliapakis/agent-skills
```

Or install a specific skill:

```bash
npx skills add giorgioliapakis/agent-skills --skill dfs-keyword-research
```

## Skills

| Skill | Description | Requires |
|-------|-------------|----------|
| [dfs-keyword-research](skills/dfs-keyword-research/) | Keyword research, SERP analysis, and competitor intelligence via DataForSEO | `npm install -g data-4-seo-cli` |
| [nb-image-generation](skills/nb-image-generation/) | Image generation, editing, restoration, icons, patterns, and diagrams via Gemini | `npm install -g @giorgioliapakis/nanobanana` |
| [meta-ads-management](skills/meta-ads-management/) | Meta (Facebook/Instagram) Ads campaign management, insights, and bulk operations | `npm install -g meta-ads-cli` |

## License

MIT
