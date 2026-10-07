[![Netlify Status](https://api.netlify.com/api/v1/badges/1f28800a-bacd-4459-a831-34a441679e6e/deploy-status)](https://app.netlify.com/projects/zheng-talks/deploys)

# talks

Slides &amp; code for my talks, using [Slidev](https://sli.dev).

## Development

Use Bun workspaces: `bun install`, then `bun run dev` to select a talk or
`bun run build` to build published talks from source. Generated sites live in `dist/`
and are ignored by Git.

Repository guidance lives in [AGENTS.md](./AGENTS.md). Shared skills live under
`.agents/skills/`: Slidev references, presentation best practices, frontend
design, and web design reviews. See the [skill inventory](./.agents/skills/README.md)
for entry points, pinned upstream versions, and update instructions.

## 📊 Metadata API

All talks metadata is available as JSON for easy integration with other projects:

**Endpoint**: [`https://zheng-talks.netlify.app/talks-metadata.json`](https://zheng-talks.netlify.app/talks-metadata.json)

Perfect for:

- Portfolio websites
- Research pages
- Next.js projects
- Automated listings

See [Quick Start Guide](./docs/QUICK_START.md) | [Full Documentation](./docs/METADATA_SYSTEM.md) | [Next.js Examples](./docs/NEXTJS_EXAMPLES.md)

---

###### 2025

- `en` [DeepRTE: Pre-trained Attention-based Neural Network for Radiative Transfer](./2025-09-20) - SHSIAM 2025, Shanghai, China
- `en` [DeepRTE: Pre-trained Attention-based Neural Network for Radiative Transfer](./2025-08-18) - CMCMS 2025, Changsha, Hunan, China
- `en` [Solve Kinetic Equations with Deep Learning](./2025-07-20) - CSIAM-BDAI 2025, Gunlin, Guangxin, China
- `en` [Solve Kinetic Equations with Deep Learning](./2025-07-10) - HKSIAM 2025, HongKong, China
