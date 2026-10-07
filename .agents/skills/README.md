# Repository Skills

All project skills live here as ordinary files under `.agents/skills/`. Read
each skill's `SKILL.md` when its purpose matches the task. The repository's
[AGENTS.md](../../AGENTS.md) supplies project conventions and routing.

## Skill Selection

| Skill                                                   | Use it for                                                                         |
| ------------------------------------------------------- | ---------------------------------------------------------------------------------- |
| [slidev](slidev/SKILL.md)                               | Slidev syntax, configuration, components, animations, CLI, and exports             |
| [slidev-best-practices](slidev-best-practices/SKILL.md) | Narrative, readable technical slides, deck structure, browser review, and delivery |
| [frontend-design](frontend-design/SKILL.md)             | Visual direction, typography, palette, composition, and intentional UI styling     |
| [web-design-guidelines](web-design-guidelines/SKILL.md) | Requested design/accessibility reviews of slides, custom controls, and web UI      |

For a new deck, start with `slidev` and `slidev-best-practices`; add design skills
when their scope is relevant. A small syntax correction does not require a full
design workflow. User preferences and the existing talk's identity take
precedence over generic aesthetic defaults.

## Verified Sources

Checked on **2026-10-07**, using each repository's default-branch HEAD at the
time of retrieval. These are pinned snapshots, with repository adaptations
listed below, rather than an automatically updating installation.

| Skill                 | Upstream snapshot                                                                                                                                                 | Upstream commit date | License                                                     |
| --------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------- | ----------------------------------------------------------- |
| slidev                | [slidevjs/slidev · 73053ab2b965](https://github.com/slidevjs/slidev/tree/73053ab2b9653ed475960301b56e1ce4439d9c75/skills/slidev)                                  | 2026-10-02           | [MIT](slidev/LICENSE.txt)                                   |
| frontend-design       | [anthropics/skills · 683bc88e56f3](https://github.com/anthropics/skills/tree/683bc88e56f3e09ba94f7055977f3d3aa499f202/skills/frontend-design)                     | 2026-10-05           | [Apache-2.0](frontend-design/LICENSE.txt)                   |
| web-design-guidelines | [vercel-labs/agent-skills · 063bee94c3f4](https://github.com/vercel-labs/agent-skills/tree/063bee94c3f4df8453406c830b0a7df0f2860278/skills/web-design-guidelines) | 2026-08-28           | [Upstream MIT declaration](web-design-guidelines/NOTICE.md) |
| slidev-best-practices | Maintained in this repository                                                                                                                                     | —                    | Repository-local guidance                                   |

The Vercel skill fetches its review rules separately on each use. The live
[Web Interface Guidelines](https://github.com/vercel-labs/web-interface-guidelines/blob/434b7f91364665f2f733b310ec54809bf8f37937/command.md)
were also checked on 2026-10-07 at commit `434b7f913646` (2026-10-05), including
media alternatives, gesture alternatives, and controls for prolonged autoplay.
This records the verification snapshot; reviews should still fetch current rules.

The root [skills-lock.json](../../skills-lock.json) records source locations,
pinned refs, and hashes of the installed skill folders. The local best-practices
skill has a `local` source entry. Folder hashes follow the
[skills CLI algorithm](https://github.com/vercel-labs/skills/blob/main/src/local-lock.ts):
SHA-256 of relative file paths and contents sorted with JavaScript `localeCompare`,
excluding nested `.git` and `node_modules` directories.

## Repository Adaptations

- **Slidev:** Bun workspace commands, `.agents` links, the corrected draggable
  reference, client-neutral MCP setup, and export guidance are preserved. The
  current upstream adds magic-move options, Tweet URL input, and an editable
  PPTX format to its references. Newer APIs are labeled where Slidev 52.19.1
  does not support them. The upstream MIT license is retained locally.
- **Frontend design:** The skill uses the supplied brief and existing talk
  instead of assuming previous rejected designs. It proceeds from available
  context and targets Slidev/Vue/UnoCSS, with canvas-aware layout guidance.
  Its upstream design principles and license are retained.
- **Web design guidelines:** Fetch instructions are tool-neutral, review targets
  can be inferred from the active task, and application-specific rules apply
  only where that UI exists. The skill still fetches Vercel's current guidelines
  before a review and reports when that fetch is unavailable.
- **Slidev best practices:** Local guidance connects narrative, scientific
  accuracy, visual choices, implementation, and rendered-output verification.
  Its recommendations are distinguished from framework requirements.

## Updating

1. Resolve and record the upstream commit before downloading a skill. Stage it
   in a temporary directory, then review its files and license notices.
2. Compare the staged source against the installed version. Merge upstream
   changes while preserving the adaptations above and all local guidance.
   A bulk reinstall can overwrite those adaptations.
3. Keep files in `.agents/skills/`; use an installer with an explicit destination
   instead of creating client-specific copies or symlinks. Updating a skill does
   not by itself call for upgrading presentation dependencies.
4. Update the pinned source refs, this inventory, and folder hashes after
   formatting. Validate skill frontmatter, local links, discoverability, and
   commands affected by the change. Include version checks for new Slidev APIs.

New skill discovery takes effect on the next chat turn. The Markdown entry
points can also be read directly when working in this repository.
