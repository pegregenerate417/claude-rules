# Claude Rules

English | [中文](README_CN.md)

Coding standards template library for AI coding assistants. Combine **base + language + framework** layers to generate a project-specific rules file that keeps AI-generated code clean and consistent.

## The Problem

AI coding assistants tend to mimic existing code style in legacy projects — including bad habits. The core principle of this library:

> **Don't imitate legacy code. Refactor according to the standards.**

Every rule is a concrete, actionable directive (not vague "use proper XX"), with "Bad / Good" code comparison examples.

## Directory Structure

```
claude-rules/
├── base/                   # Universal (required)
│   ├── core.md             # Core principles: legacy code attitude, quality metrics, naming, architecture
│   └── git.md              # Git commit message conventions
│
├── languages/              # Pick by language
│   ├── typescript.md       # No any/enum/barrel exports, as const, import type
│   ├── javascript.md       # ES2022+, JSDoc type annotations, ESM only
│   ├── java.md             # Java 17+ record/sealed/pattern matching, Optional
│   ├── kotlin.md           # Null safety, structured concurrency, sealed class
│   ├── swift.md            # guard let, async/await, actor, Protocol
│   ├── python.md           # ruff, type annotations, Protocol, uv/poetry
│   ├── html.md             # Semantic tags, accessibility, no div soup
│   └── css.md              # Custom properties, Flexbox/Grid, BEM, modern features
│
└── frameworks/             # Pick by framework
    ├── vue.md              # script setup, ref vs reactive, composable patterns
    ├── react.md            # Hooks rules, correct useEffect, state layering
    ├── swiftui.md          # @Observable (not legacy ObservableObject), SwiftData
    ├── springboot.md       # Layered architecture, DTO, global exception handling
    └── tauri.md            # Command design, service encapsulation, security config
```

## Three-Layer Architecture

```
┌─────────────────────────────────────────────┐
│              base (required)                 │  core.md + git.md
│  Legacy code attitude / Quality metrics /   │  Applies to all projects
│  Naming / Architecture                      │
├─────────────────────────────────────────────┤
│            language (pick)                   │  typescript.md / java.md / ...
│  Type system / Naming conventions /         │  Based on project language
│  Language-specific features                 │
├─────────────────────────────────────────────┤
│            framework (pick)                  │  vue.md / react.md / ...
│  Component standards / State management /   │  Based on project framework
│  Architecture patterns                      │
└─────────────────────────────────────────────┘
```

**Rule priority**: framework > language > base (specific rules override general rules)

## Usage

### Quick Start (Claude Code Plugin)

Add the marketplace and install the plugin:

```bash
claude plugin marketplace add lifedever/claude-rules
claude plugin install claude-rules-init@claude-rules
```

Then in any project, just say:

```
init rules
```

The plugin will auto-detect your tech stack, fetch the latest rules from this repo, and generate `CLAUDE.md` for you.

To update rules in the future:

```bash
claude plugin marketplace update claude-rules
```

### Manual Usage

Concatenate the rule files you need into a single file:

```bash
# Example: Vue 3 + TypeScript project
cat base/core.md base/git.md languages/typescript.md frameworks/vue.md > CLAUDE.md
```

The rules are plain Markdown and work with any AI coding tool. Just place the output where your tool expects:

| Tool | Target File |
|------|-------------|
| Claude Code | `CLAUDE.md` |
| Cursor | `.cursorrules` or `.cursor/rules/*.mdc` |
| Windsurf | `.windsurfrules` |
| GitHub Copilot | `.github/copilot-instructions.md` |

## Design Principles

1. **Actionable** — Every rule is directly executable by AI, no vague wording
2. **Exemplified** — Key rules include "Bad" and "Good" code comparisons
3. **Quantified** — Functions ≤30 lines, files ≤300 lines, nesting ≤3 levels, parameters ≤4
4. **Up-to-date** — Uses modern APIs for each language/framework (@Observable, record, as const, etc.)
5. **Not hollow** — Instead of "handle errors properly", specifies exactly how to handle them

## Contributing

PRs for new languages or frameworks are welcome. Please follow these guidelines:

- Rules must be concrete and actionable — no "use appropriate/proper" phrasing
- Key rules should include code examples (bad practice + good practice)
- Recommend modern idioms — don't document outdated APIs
- Write in English

## References

- [flyeric0212/cursor-rules](https://github.com/flyeric0212/cursor-rules) — Cursor IDE rules template library

## License

[MIT](LICENSE)
