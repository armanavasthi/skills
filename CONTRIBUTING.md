# Contributing to Skills

Thank you for considering contributing to the `skills` repository! This project aims to maintain a high-quality collection of modular skills for AI coding agents and LLMs.

## 📋 Skill Checklist

Before submitting a new skill, please ensure:

1. **Directory Naming**: The folder name must use `kebab-case` matching the skill name (e.g. `human-writing`, `sql-optimizer`).
2. **`SKILL.md` File**: Must be located at the root of your skill folder (`<skill-name>/SKILL.md`).
3. **YAML Frontmatter**:
   - Must start on line 1 with `---`.
   - Must contain `name` (matching directory name).
   - Must contain a clear, action-oriented `description` explaining **when** and **why** an agent should activate the skill.
4. **Content & Quality**:
   - Instructions should be actionable, clear, and unambiguous.
   - Use concrete examples, diagnostic tables, or explicit do's and don'ts.
   - Avoid vague or contradictory rules.
   - Keep instructions concise without redundant preamble.
5. **No OS / Junk Files**: Ensure files like `.DS_Store` or temporary logs are omitted.

## 🛠️ Step-by-Step Submission Process

1. **Fork the Repository**: Create your copy of the repo on GitHub.
2. **Create a Feature Branch**:
   ```bash
   git checkout -b skill/my-new-skill
   ```
3. **Add Your Skill**:
   ```bash
   mkdir my-new-skill
   touch my-new-skill/SKILL.md
   ```
4. **Commit & Push**:
   ```bash
   git add my-new-skill
   git commit -m "feat(skill): add my-new-skill"
   git push origin skill/my-new-skill
   ```
5. **Open a Pull Request**: Provide a description of what the skill does and example use cases.

Thank you for helping build a better skill library!
