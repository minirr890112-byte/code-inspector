---
name: code-inspector
description: AI-generated code quality detector — 8 smell checks (truncation, thinking leaks, hardcoded keys, missing error handling, TODO bombs, copy-paste, bare except, incomplete imports). Quality score 0-100. Supports Python/JS/TS.
version: 1.2.0
author: minirr890112-byte
license: MIT
metadata:
  hermes:
    tags: [Code-Quality, AI-Code, Linter, Security, Developer-Tools, Python, JavaScript]
    homepage: https://github.com/minirr890112-byte/code-inspector
---

# code-inspector

## Problem → Solution

**The problem**: AI writes your code. You paste it in. It runs. But did the LLM truncate halfway through? Did it leak its thinking process into a comment? Is there an API key hardcoded on line 42? You don't know until it breaks in production.

**The solution**: One command scans AI-generated code for 8 common failure patterns. Each file gets a 0-100 quality score. Critical issues (truncation, hardcoded secrets) flagged in red. No setup, no config.

## Quick Start

```bash
pip install git+https://github.com/minirr890112-byte/code-inspector.git

code-inspector check app.py
code-inspector scan ./src
code-inspector stats ./project
```

## Real Output

```
$ code-inspector check app.py

╭────────────── Code Inspector ──────────────╮
│ app.py  |  Language: Python                 │
╰─────────────────────────────────────────────╯
Quality Score: ████████████████░░░░ 80/100

╭────────── Smells Found: 2 ──────────╮
│ # │ Line │ Severity  │ Type         │
├───┼──────┼───────────┼──────────────┤
│ 1 │  42  │ 🔴 crit   │ hardcoded key│
│ 2 │  15  │ 🟡 warn   │ todo bomb    │
╰──────────────────────────────────────╯
```

## 8 Detectors

| # | Smell | Severity | Penalty |
|---|-------|----------|---------|
| 1 | Truncated code (`// ...`, `# rest of`) | 🔴 Critical | -20 |
| 2 | Thinking leak (`// Let me`, `# First,`) | 🟡 Warning | -15 |
| 3 | Hardcoded secret (API key, token) | 🔴 Critical | -25 |
| 4 | Missing error handling (no try/except) | 🟡 Warning | -10 |
| 5 | TODO bomb (>3 TODOs) | 🟡 Warning | -8 |
| 6 | Copy-paste (>5 duplicate lines) | 🟡 Warning | -12 |
| 7 | Incomplete import (`pd`, `np` undefined) | 🔵 Info | -10 |
| 8 | Bare except (no exception type) | 🟡 Warning | -7 |

---
⭐ **Star this repo if it caught a bug before production**: [github.com/minirr890112-byte/code-inspector](https://github.com/minirr890112-byte/code-inspector)
