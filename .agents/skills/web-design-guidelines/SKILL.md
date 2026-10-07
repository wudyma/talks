---
name: web-design-guidelines
description: Review UI code for Web Interface Guidelines compliance. Use when asked to "review my UI", "check accessibility", "audit design", "review UX", or "check my site against best practices".
metadata:
  author: vercel
  version: "1.0.0"
  argument-hint: <file-or-pattern>
---

# Web Interface Guidelines

<!-- Locally adapted from vercel-labs/agent-skills: portable tools, inferred targets, and Slidev review scope. See ../README.md for provenance. -->

Review files for compliance with Web Interface Guidelines.

## How It Works

1. Fetch the latest guidelines from the source URL below
2. Read the specified files, or infer the target from the active talk and changes
3. Check the rules applicable to those files and the requested scope
4. Report actionable findings with file paths, line numbers, impact, and a fix

## Guidelines Source

Fetch fresh guidelines before each review:

```
https://raw.githubusercontent.com/vercel-labs/web-interface-guidelines/main/command.md
```

Use the available web or HTTP fetch tool to retrieve the latest rules. If the
source is unavailable, state that the live guidelines could not be checked;
continue with any rules already available and do not claim a current full review.

## Slidev Review Scope

For presentations, combine this review with
[slidev-best-practices](../slidev-best-practices/SKILL.md). Check the rendered
canvas for readability, clipping, contrast, image descriptions, click states,
and reduced motion. Check keyboard focus and labels on custom interactive
components. Apply forms, responsive navigation, and other application rules
only where that UI exists. Preserve Slidev's canvas scaling and slide navigation.
Use Vue/HTML equivalents for framework-specific examples; no React migration is
implied. Follow the user's language and branding when stylistic rules conflict.

## Usage

When a user provides a file or pattern argument:

1. Fetch guidelines from the source URL above
2. Read the specified files
3. Apply relevant rules from the fetched guidelines
4. Group actionable findings by file; include verified line references

If the target cannot be inferred from the request or current work, ask for the
files or talk to review. When the user requested implementation or fixes,
complete the relevant corrections instead of stopping at an audit report.
