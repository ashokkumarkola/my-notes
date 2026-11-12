# Note Templates

Copy-paste skeletons for new notes. Delete sections that do not fit. Never keep empty headings.

| Template | Use for | Example |
|---|---|---|
| [Concept note](#1-concept-note) | Explaining a technology or idea | `cloud/aws/iam.md` |
| [Command cheat sheet](#2-command-cheat-sheet) | Commands grouped by task | `git/git-commands.md` |
| [How-to guide](#3-how-to-guide) | Step-by-step setup or procedure | `git/add-ssh-keys.md` |
| [Section index](#4-section-index) | `index.md` of a folder | `cloud/index.md` |

Syntax for each element: [Format Guide](mkdocs-format-guide.md).

---

## 1. Concept note

````markdown
---
tags:
  - topic
---

# Topic Name

One-line summary: what it is and why it matters.

## Overview

- What: ...
- Why: problem it solves.
- When: typical use cases.

## Core concepts

| Term | Meaning |
|---|---|
| ... | ... |

## How it works

```mermaid
flowchart LR
    A --> B --> C
```

Short explanation of the flow.

## Example

```python
# minimal working example
```

## Gotchas

!!! warning
    Common mistake and fix.

## Comparison

| | Option A | Option B |
|---|---|---|
| Use when | ... | ... |

## Quick revision

- Point 1
- Point 2
- Point 3

## Interview questions

??? question "Question?"
    Answer.

## Related

- [Related note](../other/note.md)

## References

- [Official docs](https://...)
````

---

## 2. Command cheat sheet

````markdown
# Tool Commands

One-line summary of the tool.

## Quick reference

| Task | Command |
|---|---|
| ... | `...` |

## 1. Setup

```bash
tool --version
```

## 2. Daily use

```bash
tool do-thing      # what it does
```

## 3. Advanced

```bash
tool advanced --flag   # when to use
```

## Dangerous commands

!!! danger
    `tool destroy` deletes data permanently. Back up first.

## References

- [Official docs](https://...)
````

---

## 3. How-to guide

````markdown
# How to Do X

Goal: end state in one line.

## Prerequisites

- Tool A installed
- Access to B

## Steps

### 1. First step

```bash
command one
```

Why: one-line reason.

### 2. Second step

```bash
command two
```

## Verify

```bash
check-command      # expected output: ...
```

## Troubleshooting

| Problem | Fix |
|---|---|
| `exact error text` | fix |

## Rollback

```bash
undo-command
```
````

---

## 4. Section index

````markdown
# Section Name

One-line description of what this section covers.

- [Page one](page-one.md): short description
- [Page two](page-two.md): short description
- [Subsection](subsection/index.md): short description
````

After Phase 4, use grid cards instead of a list: see [Format Guide → Grid cards](mkdocs-format-guide.md#13-grid-cards-dashboard-layout).
