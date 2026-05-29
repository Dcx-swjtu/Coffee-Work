# Coffee Work

Coffee Work is a Hermes plugin and reusable skill for coordinating local coding
CLIs such as Codex, Kimi Code, Claude Code, OpenCode, Gemini CLI, and tmux-backed
sessions.

It gives Hermes a practical workflow for choosing the right backend, sending a
scoped task prompt, monitoring execution, collecting evidence, and reporting
commands, diffs, artifacts, tests, failures, and remaining risks.

[中文说明](README_zh.md)

## Install

Install the plugin from this repository:

```bash
hermes plugins install https://github.com/Dcx-swjtu/Coffee-Work --enable
```

Then use it inside Hermes:

```text
/coffee-work Use Codex to review my current diff. Read-only. Focus on bugs, security risks, and missing tests.
```

If you only want the skill file:

```bash
hermes skills install https://raw.githubusercontent.com/Dcx-swjtu/Coffee-Work/main/SKILL.md --name coffee-work
```

## Why Coffee Work

Multi-agent coding work often spans more than one terminal assistant:

- Codex for focused implementation and debugging.
- Claude Code for careful review passes.
- Kimi Code for long-context repository understanding.
- OpenCode for local project navigation.
- Gemini CLI for quick inspection and lightweight review.
- tmux or similar tools for long-lived interactive sessions.

Without a bridge, the user becomes the router: copying prompts, tracking which
terminal has context, checking whether tests actually ran, and pasting summaries
back into the main assistant. Coffee Work makes that workflow explicit and
evidence-driven.

## What It Does

Coffee Work teaches Hermes to:

- discover installed local coding CLIs;
- choose the backend, working directory, and session intentionally;
- reuse existing sessions when appropriate;
- build prompts with role, background, task, constraints, success criteria, and
  report format;
- run the real requested CLI instead of substituting another assistant;
- monitor long-running jobs through terminal, tmux, or process logs;
- collect raw output, diffs, artifacts, and verification results;
- report what actually happened, including failures and uncertainty.

## Example Requests

Implementation and review:

```text
/coffee-work Use Codex to implement the smallest fix for this failing test. Then use Claude Code as a read-only reviewer. Report both agents' evidence.
```

Second opinion:

```text
/coffee-work Use a different local coding agent to review my latest diff. Do not edit files. Look for correctness bugs, security issues, and test gaps.
```

Long-context repository understanding:

```text
/coffee-work Use Kimi Code to inspect this repository and explain where this feature should live. Read-only.
```

Existing session continuation:

```text
/coffee-work Continue the existing Codex session for this project. Do not start a new session unless no matching session exists.
```

## Safety Model

Coffee Work is intentionally strict about evidence and side effects:

- report the exact command or session used;
- avoid leaking secrets, private paths, real session IDs, or private project names
  in public output;
- ask before risky actions such as pushing commits, deleting data, spending
  money, or bypassing sandbox controls;
- avoid editing coding-agent databases, transcripts, or hidden session internals;
- verify files, artifacts, and tests before claiming success;
- say when a task is blocked instead of inventing a successful result.

## Repository Layout

```text
Coffee-Work/
  README.md
  README_zh.md
  LICENSE
  plugin.yaml
  __init__.py
  after-install.md
  SKILL.md
```

## Public Release Check

Before publishing changes, scan the repository for accidental private data:

```bash
rg -n "(/Users/|/home/|API_KEY|TOKEN|SECRET|PRIVATE|@)" .
```

Review every match manually. Placeholders may be intentional; real secrets,
private paths, and private account identifiers should not be committed.

## License

MIT
