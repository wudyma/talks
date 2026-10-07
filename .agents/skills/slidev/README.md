# Slidev Agent Skill

Shared repository skill for creating and editing [Slidev](https://sli.dev) presentations.

## Location

```text
.agents/skills/slidev/
├── SKILL.md       # Skill entry point and repository workflow
└── references/    # Slidev feature references
```

The skill is checked into this repository. Use [SKILL.md](SKILL.md) as the entry
point and follow [AGENTS.md](../../../AGENTS.md) for repository conventions.

For deck authoring and visual quality, pair it with
[slidev-best-practices](../slidev-best-practices/SKILL.md). See the
[skill inventory](../README.md) for upstream versions and design companion skills.

## What's Included

The Slidev skill covers:

- **Core Syntax** - Markdown syntax, slide separators, frontmatter
- **Animations** - Click animations, transitions, motion effects
- **Code Features** - Line highlighting, Monaco editor, code groups, magic-move
- **Diagrams** - Mermaid, PlantUML, LaTeX math
- **Layouts** - Built-in layouts, slots, global layers
- **Presenter Mode** - Recording, timer, remote access
- **Exporting** - PDF, PPTX, PNG, SPA hosting

## Usage

Agents can use this skill when:

- Creating new presentations
- Adding slides with code examples
- Setting up animations and transitions
- Configuring themes and layouts
- Exporting presentations

### Example Prompts

```
Create a Slidev presentation about TypeScript generics with code examples
```

```
Add a two-column slide with code on the left and explanation on the right
```

```
Set up click animations to reveal bullet points one by one
```

```
Configure the presentation for PDF export with speaker notes
```

## Documentation

- [Slidev Documentation](https://sli.dev)
- [Theme Gallery](https://sli.dev/resources/theme-gallery)
- [Showcases](https://sli.dev/resources/showcases)

## License

MIT
