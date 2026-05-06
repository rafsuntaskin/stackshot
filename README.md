# StackShot

![StackShot tech stack card](stackshot.png)

StackShot is an agent skill that scans a repository and generates a polished 1200x630 image-generation prompt for a tech stack card.

It collects project metadata, framework and language signals, file counts, LOC, tests, key tools, language breakdown, and optional repo styling guidance.

Want to copy/paste the prompt manually? Open [STACKSHOT.md](STACKSHOT.md).

## Install For Codex

### Install From GitHub

Install StackShot directly from the plugin repository:

```bash
codex plugin add github:rafsuntaskin/stackshot
```

StackShot exposes the installable skill from:

```text
plugins/stackshot/skills/stackshot/SKILL.md
```

Restart Codex or start a new session so the skill can be discovered.

### Install From The Marketplace

Add the `ai-plugins` marketplace:

```bash
codex plugin marketplace add rafsuntaskin/ai-plugins
```

Then install StackShot from that marketplace:

```bash
codex plugin add stackshot
```

The marketplace entry points to:

```text
github:rafsuntaskin/stackshot
```

## Usage

Ask Codex something like:

```text
Use StackShot to generate a tech stack card prompt for this repo.
```

or:

```text
Generate a dark glass StackShot card prompt for this project.
```

If your agent supports plugin slash commands, use:

```text
/stackshot
```

or with a style:

```text
/stackshot minimal
```

Skills are usually model-invoked: the agent decides to use StackShot when your request matches the skill description. The slash command is a convenience wrapper that explicitly asks the agent to run the StackShot workflow.

StackShot scans the current repository and collects:

- Project name
- Primary framework and language
- Key tools and dependencies
- Source file count
- Lines of code
- Test count
- Top language breakdown
- Optional brand or design-system styling signals

If you do not specify a style, StackShot asks you to choose one:

```text
default
dark glass
neon
minimal
brutalist
cyberpunk
terminal
```

Use `default` when you want StackShot to inspect the repository's own CSS, theme files, design tokens, assets, README, or brand docs and infer a visual direction.

Example prompts:

```text
Use StackShot for this repo and use the default style.
```

```text
Generate a minimal StackShot prompt for this project.
```

```text
Scan this repository and create a cyberpunk tech stack card prompt.
```

```text
Use StackShot, but set the project name to "Acme Dashboard".
```

The skill outputs a final image-generation prompt for a 1200x630 tech stack card. Paste that prompt into your preferred image model or image-generation tool.

## Marketplace Repository

StackShot is listed in:

```text
rafsuntaskin/ai-plugins
```

The marketplace file is:

```text
.claude-plugin/marketplace.json
```
