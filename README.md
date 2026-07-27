# Skills 🧠

A curated collection of production-grade, modular skills and instructions for AI agents and LLM assistants (compatible with [Google Antigravity](https://github.com/google/antigravity), AGY CLI, Cursor, Claude, ChatGPT, and custom LLM agent frameworks).

## 📌 Overview

Skills are self-contained instructions, domain workflows, and procedural knowledge rules packaged for AI agents. They provide structured guidance on specific domains—ranging from natural writing to system design and code refactoring—allowing autonomous agents to execute complex tasks predictably and consistently.

---

## 🗂️ Available Skills

| Skill Name | Description | SKILL Spec |
| :--- | :--- | :--- |
| [**human-writing**](./human-writing) | Draft and revise prose so it sounds natural, specific, purposeful, and appropriate to its author and audience. Eliminates formulaic AI tropes, fluff, and robotic phrasing while preserving factual accuracy. | [`human-writing/SKILL.md`](./human-writing/SKILL.md) |

---

## 📂 Repository Structure

```
skills/
├── human-writing/
│   └── SKILL.md
├── CONTRIBUTING.md
├── LICENSE
└── README.md
```

---

## 🚀 How to Use

### 1. Installing Skills for Google Antigravity / AGY CLI

To use these skills with Antigravity or AGY CLI:

1. Clone or copy the desired skill directory to your local skills location:
   ```bash
   cp -r human-writing ~/.gemini/config/skills/
   ```
2. The agent will automatically discover the skill via its YAML frontmatter `name` and `description`.

### 2. Manual / Prompt Injection

You can also reference or copy the contents of `SKILL.md` directly into custom system prompts, AGY rule files, or instructions for any LLM workspace.

---

## ✍️ Skill Format Specification

Each skill directory must contain a `SKILL.md` file formatted as follows:

```yaml
---
name: skill-name
description: A concise description of when and why the agent should activate this skill.
---

# Skill Title

## Guidance & Rules
...
```

For more complex skills, optional subdirectories can be added:
- `references/` — Extended technical specs or background documentation.
- `scripts/` — Helper scripts or automation utilities for the skill.
- `examples/` — Sample inputs/outputs demonstrating expected skill behavior.

---

## 🤝 Contributing

Contributions are welcome! If you've created a custom skill that improves AI agent behavior:

1. Fork this repository.
2. Create a new directory for your skill (use `kebab-case`).
3. Add a valid `SKILL.md` file with YAML frontmatter.
4. Open a Pull Request.

Please see [CONTRIBUTING.md](./CONTRIBUTING.md) for detailed guidelines.

---

## 📄 License

This repository is licensed under the [MIT License](./LICENSE).
