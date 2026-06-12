# Solana Finance

A Claude Code plugin for creating and editing Solana projects, including Rust/Anchor/Quasar and TypeScript, with a focus on:

- Maintainability
- Readability
- Minimal code
- Financial math
- 2026 best practices

This skill has the **most stars of any ecosystem Solana Claude skill** and is made by someone working in the software industry for more than 25 years, based on production-code used by some of the largest programs on Solana. 

Made by [Quicknode](https://quicknode.com).

> [!TIP]
> If you find this plugin useful, please add a GitHub star above! 🙏 

## What is this?

**Solana Finance** is a Claude Code plugin that bundles the `solana` skill — a reusable instruction set Claude automatically applies when working on Solana code, or that you can invoke manually. Skills are triggered automatically based on context (e.g. opening an Anchor program or a Solana Kit client).

## Installation

### As a plugin (recommended)

Once the plugin is published, install it from the marketplace:

```
/plugin install solana-finance
```

### As a standalone skill

You can also install just the skill directly:

```bash
npx skills add https://github.com/quicknode/solana-claude-skill
```

This installs the skill to your Claude Code skills directory (`~/.claude/skills/`).

## Usage

Once installed, the skill automatically applies when Claude Code works on Solana/Anchor/Quasar projects. You can also invoke it manually:

```
/solana-finance:solana
```

(When installed as a standalone skill rather than via the plugin, invoke it with `/solana`.)

## Repository layout

```
.claude-plugin/plugin.json   # Plugin manifest (name, author, version)
skills/solana/               # The skill
  SKILL.md                   # Skill entry point + general guidelines
  ANCHOR.md  RUST.md  QUASAR.md  TYPESCRIPT.md   # Language/framework references
```
