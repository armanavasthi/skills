---
name: trim-prompt
description: Compresses user-provided prompts, logs, code, and documentation to significantly cut token usage before sending them to another coding LLM (Codex, Claude Code, Gemini CLI, Antigravity, or similar). Use this whenever the user asks to trim, compress, shrink, condense, or reduce a prompt, terminal output, stack trace, log file, or piece of documentation to save tokens or make it easier to paste elsewhere, even if they don't say "compress" outright, e.g. "clean up this log before I paste it into Codex", "shrink this doc", "cut the noise out of this trace".
---

# trim-prompt

## Purpose

Compress user-provided content to significantly reduce token usage while preserving the information that matters for another LLM (Codex, Claude Code, Gemini CLI, Antigravity, etc.).

Detect whether the input is primarily:

- Terminal/log output
- Source code
- Prose/documentation
- Mixed (logs + prose + code)

Apply the appropriate compression strategy automatically.

---

## Core Principles

- Optimize for **maximum token reduction with minimal information loss**.
- Preserve execution flow, important decisions, and observable behavior.
- Remove noise, not information.
- Prefer omission over rewriting for logs and code.
- Prefer rewriting over omission for prose.
- Never invent or infer information that was not present.

---

# Mode 1: Terminal / Log Compression

Treat shell output, terminal logs, server logs, stack traces, build logs, Kubernetes logs, Docker logs, HTTP logs, etc. as structured evidence.

## Preserve Exactly

If a line is kept, **do not modify it**.

Preserve:

- commands
- prompts
- user inputs
- errors
- warnings
- important informational messages
- state transitions
- graph/node transitions
- routing decisions
- tool invocations
- API/function names
- queries
- rewritten queries
- configuration values
- final outputs
- summaries
- timings (when meaningful)

Keep indentation, ordering, and relative sequence. Never rewrite kept lines.

Example:

Instead of

```text
python main.py ingest docs/a.txt
```

Never output

```text
Executed ingestion command.
```

The original line must remain unchanged.

## Remove

Aggressively remove repetitive, low-information content such as:

- repeated HTTP requests
- repeated INFO/DEBUG logs
- timestamps
- session IDs
- request IDs
- ports
- repeated health checks
- download progress
- model download logs
- progress bars
- repeated initialization messages
- duplicate status messages
- verbose framework logging
- transport noise

## Replace Removed Sections

Replace contiguous removed sections with a concise placeholder.

Examples:

```text
...
```

```text
... (HTTP requests omitted)
```

```text
... (model initialization)
```

```text
... (repeated INFO logs)
```

Avoid excessive placeholders. If multiple adjacent sections are removed, prefer one placeholder.

## Never Collapse

Never remove or rewrite: shell commands, user questions, assistant responses, stack traces that explain failures, exception messages, tool names, function names, graph decisions, workflow transitions, configuration values, or outputs returned to the user.

---

# Mode 2: Source Code Compression

Treat source code the way Mode 1 treats logs: as evidence to preserve, not prose to rewrite. Rewriting code, even lightly, risks silently changing its meaning, so compression here means cutting what's redundant, not rephrasing what remains.

## Preserve Exactly

Never modify, reformat, or paraphrase:

- function and class definitions
- logic, control flow, and algorithms
- variable names, types, and signatures
- imports and dependencies
- any line that affects runtime behavior

## Remove

- large blocks of generated or boilerplate code that repeat a pattern already shown once (e.g. ten near-identical getter/setter methods; keep one or two as representative, note the rest are elided)
- long stretches of commented-out dead code
- verbose comments that just restate what the next line obviously does
- repeated import blocks or license headers across multiple pasted files

Replace removed sections with a placeholder that states what was cut, e.g. `... (8 similar getters omitted)`.

If you are unsure whether a block is safe to remove without losing meaning, keep it. Under-compressing code is a minor cost; over-compressing it can break the recipient's understanding of the program.

---

# Mode 3: Prose Compression

Rewrite for clarity and brevity.

Goals: preserve meaning, remove redundancy, remove filler, simplify wording, shorten long sentences, improve readability.

Allowed: rewrite, merge sentences, convert to bullets, simplify wording.

Not allowed: change meaning, remove important facts, introduce new information.

---

# Mode 4: Mixed Content

Many prompts contain logs, code, and prose together.

Apply:

- Terminal rules (Mode 1) inside logs/terminal blocks.
- Source code rules (Mode 2) inside code blocks.
- Prose rules (Mode 3) everywhere else.

Do not rewrite terminal output or code. Do not leave prose unnecessarily verbose.

---

# Compression Heuristics

Keep: execution flow, cause → effect, important milestones, architectural decisions, inputs, outputs, failures, recoveries, final state.

Compress: repetitive activity, verbose networking, repetitive framework logging, download noise, progress indicators, repeated status updates, repeated boilerplate code.

---

# Output Style

Produce only the compressed version. Do not explain what was removed. Do not add commentary. Do not describe your reasoning. Do not add notes unless explicitly requested.

---

# Goal

Transform verbose content into a concise version that preserves everything another coding LLM needs to understand the behavior while using substantially fewer tokens.
