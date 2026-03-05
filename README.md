# Shaping Skills

A [Claude Code](https://claude.com/claude-code) plugin for shaping and breadboarding — the methodology from [Shape Up](https://basecamp.com/shapeup) adapted for working with an LLM.

Reimplemented as a Claude Code plugin from [rjs/shaping-skills](https://github.com/rjs/shaping-skills) by [Ryan Singer](https://github.com/rjs), which used the earlier standalone skills format.

## Skills

**`/shaping`** — Iterate on both the problem (requirements) and solution (shapes) before committing to implementation. Separates what you need from how you might build it, with fit checks to see what's solved and what isn't.

**`/breadboarding`** — Map a system into UI affordances, code affordances, and wiring. Shows what users can do and how it works underneath — in one view. Good for slicing into vertical scopes.

**`/breadboard-reflection`** — Review a breadboard for design smells. Trace user stories through wiring, apply the naming test, and fix affordance boundary problems.

## Install

### From GitHub

Add the repo as a marketplace, then install the plugin:

```bash
claude plugin marketplace add phjlljp/shapeup
claude plugin install shapeup
```

### Local development

Clone the repo and add it as a local marketplace:

```bash
git clone https://github.com/phjlljp/shapeup.git
claude plugin marketplace add /path/to/shapeup
claude plugin install shapeup
```

Changes you make locally will take effect the next time you start Claude Code.

## Hook: Ripple Check

The plugin includes a PostToolUse hook that fires after every `Write` or `Edit` tool call. When the edited file is a `.md` with `shaping: true` in its frontmatter, it prompts a ripple-check reminder — update affordance tables, fit checks, work streams, etc.

The hook is registered automatically via `hooks/hooks.json` when the plugin is installed. No manual setup is needed.

## Plugin Structure

```
shapeup/
├── .claude-plugin/
│   └── plugin.json
├── skills/
│   ├── shaping/
│   │   ├── SKILL.md
│   │   └── references/
│   ├── breadboarding/
│   │   ├── SKILL.md
│   │   └── references/
│   └── breadboard-reflection/
│       ├── SKILL.md
│       └── references/
├── hooks/
│   ├── hooks.json
│   └── scripts/
│       └── shaping-ripple.sh
└── CHANGELOG.md
```

## Attribution

The shaping and breadboarding methodology comes from [Shape Up: Stop Running in Circles and Ship Work that Matters](https://basecamp.com/shapeup) by Ryan Singer. The book is freely available online.

The original skills were created by [Ryan Singer](https://github.com/rjs) as [shaping-skills](https://github.com/rjs/shaping-skills), using Claude Code's standalone skills format. This repo reimplements them as a plugin with auto-discovery, hook registration, and progressive disclosure via reference files. See Ryan's [walkthrough](https://x.com/rjs/status/2020184079350563263) of the full shaping process with Claude Code.
