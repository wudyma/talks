# Talks Metadata System

This system automatically collects and manages metadata for all talks/presentations in this repository.

## Features

- 🔍 **Automatic Extraction**: Extracts metadata from slides frontmatter
- 📝 **Manual Configuration**: Support custom metadata via `metadata.json` files
- 🔄 **Auto-update**: GitHub Actions automatically updates metadata on push
- 🌐 **Easy Access**: Exposed as static JSON for consumption by other projects

## Architecture

### 1. Metadata Schema

Defined in [`types/metadata.ts`](../types/metadata.ts):

```typescript
interface TalkMetadata {
  id: string; // Unique identifier (folder name)
  title: string; // Talk title
  date: string; // ISO 8601 date
  speaker?: string; // Speaker name
  affiliation?: string; // Speaker organization
  conference?: string; // Conference/event name
  location?: string; // Conference location
  language?: string; // Presentation language
  slidesUrl?: string; // Hosted slides URL
  pdfUrl?: string; // Deployed /<talk>/slides.pdf URL for published talks
  sourceUrl?: string; // Source code URL
  description?: string; // Brief description
  tags?: string[]; // Topics/tags
  collaborators?: string[]; // Co-authors
  published?: boolean; // Publication status
  custom?: Record<string, any>; // Custom fields
}
```

### 2. Collection Script

[`scripts/collect-metadata.ts`](../scripts/collect-metadata.ts) scans all talk directories and:

- Extracts frontmatter from `slides.md`
- Loads optional `metadata.json` config
- Generates URLs based on deployment structure
- The metadata CLI writes `public/talks-metadata.json`; production builds write
  `dist/talks-metadata.json`.

### 3. Auto-update Workflow

[`.github/workflows/update-metadata.yml`](../.github/workflows/update-metadata.yml):

- Triggers on push to `main` when talks change
- Runs collection script
- Commits updated metadata back to repo

## Usage

### Adding Metadata to a Talk

Create `metadata.json` in your talk directory:

```json
{
  "conference": "ICML 2025",
  "location": "Vienna, Austria",
  "description": "A brief description of the talk",
  "tags": ["machine-learning", "optimization"],
  "collaborators": ["Jane Doe", "John Smith"],
  "published": true,
  "custom": {
    "award": "Best Paper"
  }
}
```

### Manual Collection

Run the script locally:

```bash
bun run scripts/collect-metadata.ts
```

### Accessing Metadata

The metadata is available at:

- **Static JSON**: `https://zheng-talks.netlify.app/talks-metadata.json`
- **Repository**: `public/talks-metadata.json`
- **Build output**: `dist/talks-metadata.json` (ignored by Git)

## Next.js Integration

### Method 1: Static Generation (Recommended)

Fetch at build time for optimal performance:

```typescript
// app/talks/page.tsx
import type { TalksCollection } from '@/types/metadata'

async function getTalks(): Promise<TalksCollection> {
  const res = await fetch('https://zheng-talks.netlify.app/talks-metadata.json', {
    next: { revalidate: 3600 } // Revalidate every hour
  })
  return res.json()
}

export default async function TalksPage() {
  const { talks } = await getTalks()

  return (
    <div>
      <h1>Talks & Presentations</h1>
      {talks.map(talk => (
        <div key={talk.id}>
          <h2>{talk.title}</h2>
          <p>{talk.date} - {talk.conference}</p>
          <a href={talk.slidesUrl}>View Slides</a>
        </div>
      ))}
    </div>
  )
}
```

### Method 2: Client-Side

For dynamic updates:

```typescript
'use client'

import { useEffect, useState } from 'react'
import type { TalksCollection } from '@/types/metadata'

export default function TalksList() {
  const [talks, setTalks] = useState<TalksCollection | null>(null)

  useEffect(() => {
    fetch('https://zheng-talks.netlify.app/talks-metadata.json')
      .then(res => res.json())
      .then(data => setTalks(data))
  }, [])

  if (!talks) return <div>Loading...</div>

  return (
    <div>
      {talks.talks.map(talk => (
        <TalkCard key={talk.id} talk={talk} />
      ))}
    </div>
  )
}
```

### Method 3: API Route

Create a Next.js API route as proxy:

```typescript
// app/api/talks/route.ts
import { NextResponse } from "next/server";

export async function GET() {
  const res = await fetch(
    "https://zheng-talks.netlify.app/talks-metadata.json",
    {
      next: { revalidate: 3600 },
    },
  );
  const data = await res.json();

  return NextResponse.json(data);
}
```

Then use in your components:

```typescript
const talks = await fetch("/api/talks").then((r) => r.json());
```

## TypeScript Support

Copy the types to your Next.js project:

```bash
# From your Next.js project
curl -o types/talks-metadata.ts https://raw.githubusercontent.com/mazhengcn/talks/main/types/metadata.ts
```

Or install as a git submodule for automatic updates.

## CORS Configuration

The metadata JSON is served with CORS enabled on Netlify. If you need custom CORS settings, add to `netlify.toml`:

```toml
[[headers]]
for = "/talks-metadata.json"

[headers.values]
Access-Control-Allow-Origin = "https://your-nextjs-site.com"
```

## Filtering and Searching

Example utilities for your Next.js app:

```typescript
// utils/talks.ts
import type { TalkMetadata, TalksCollection } from "@/types/metadata";

export function filterByTag(talks: TalkMetadata[], tag: string) {
  return talks.filter((talk) => talk.tags?.includes(tag));
}

export function filterByYear(talks: TalkMetadata[], year: number) {
  return talks.filter((talk) => talk.date.startsWith(String(year)));
}

export function searchTalks(talks: TalkMetadata[], query: string) {
  const lowerQuery = query.toLowerCase();
  return talks.filter(
    (talk) =>
      talk.title.toLowerCase().includes(lowerQuery) ||
      talk.description?.toLowerCase().includes(lowerQuery) ||
      talk.tags?.some((tag) => tag.toLowerCase().includes(lowerQuery)),
  );
}

export function groupByYear(talks: TalkMetadata[]) {
  return talks.reduce(
    (acc, talk) => {
      const year = talk.date.split("-")[0];
      if (!acc[year]) acc[year] = [];
      acc[year].push(talk);
      return acc;
    },
    {} as Record<string, TalkMetadata[]>,
  );
}
```

## Deployment

The metadata is automatically:

1. Generated during build (`bun run build`)
2. Deployed to Netlify in the `dist` folder
3. Accessible at the base URL + `/talks-metadata.json`

## Updating URLs

Modify the URL mappings in `scripts/collect-metadata.ts`:

```typescript
const mapping: Record<string, string> = {
  "2025-07-10": "2025/hksiam",
  // Add new mappings here
};
```

## Environment Variables

- `BASE_URL`: Base URL for deployed slides (default: `https://zheng-talks.netlify.app`)

Set in GitHub Actions secrets or `.env` file for local development.
