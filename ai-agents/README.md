# AI Agents & Pipelines

This section documents how I design and use AI-powered workflows — not as a user of AI tools, but as someone who architects pipelines around them.

The focus is on agentic setups, structured prompting, and integrating AI into real operational or development processes.

---

## Philosophy

AI is most useful when it operates within a defined structure. A model that can do anything often does nothing precisely. The work here is about giving AI the right constraints, context, and output format — so it becomes a reliable component in a larger system rather than a magic box you hope works.

Key principles I work with:

- **Structured output first**: prompts are designed around what the output needs to look like, not just what the question is
- **Role clarity**: each agent in a pipeline has one job; handoffs are explicit
- **Validation at the boundary**: AI output is always treated as input that needs checking before acting on it
- **XML prompt engineering**: for complex instructions, XML structure outperforms prose — clearer hierarchy, less ambiguity

---

## Tooling

| Tool | Use |
|------|-----|
| Claude Code | Primary agent for code, architecture, and process logic |
| Codex | Code generation and refactoring assistance |
| Custom pipelines | Multi-step agentic flows with structured I/O |

---

## Areas of Application

### Development Workflows
AI agents used to audit code, validate architecture decisions, catch naming drift, and run smoke tests against a repository's own documentation.

### Operations Support
Structured prompts that process claim data, flag edge cases, and generate formatted reports — reducing manual processing time on repetitive analytical tasks.

### Documentation & Knowledge Management
Pipelines that extract structured information from unstructured input (emails, reports, specifications) and convert it into standardized formats.

---

## What's Documented Here

- [use-cases.md](./use-cases.md) — specific pipelines and patterns, described conceptually

---

> *The goal isn't automation for its own sake. It's removing friction from work that matters.*
