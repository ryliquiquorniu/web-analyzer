# Web Analyzer

Instant website analysis for Claude Code and OpenClaw. Get tech stack detection, SEO audit, accessibility check, and content summary in one command.

## Features

- **Tech Stack Detection** — Identify frameworks, libraries, CDNs, and hosting from HTML fingerprints
- **JS Deep Analysis** — Parse and evaluate JavaScript to detect SPAs, SSR frameworks, and dynamic configurations that static HTML analysis misses
- **API Endpoint Discovery** — Extract `fetch()` / `axios` / `XHR` calls from JS and verify endpoint liveness
- **SEO Audit** — Title, meta description, Open Graph, canonical URL, structured data (JSON-LD)
- **Accessibility Check** — Alt text coverage, ARIA usage, heading hierarchy
- **Content Summary** — Word count, key topics, internal/external link inventory
- **Batch Analysis** — Analyze multiple URLs in one session

## Install

### From ClawHub

```bash
clawhub install web-analyzer
```

### From GitHub (Claude Code)

```bash
claude --skill https://raw.githubusercontent.com/ryliquiquorniu/web-analyzer/main/SKILL.md
```

### From GitHub (OpenClaw)

```bash
openclaw install --from-github ryliquiquorniu/web-analyzer
```

### Manual

Download `SKILL.md` and place it in your skills directory:

```bash
# Claude Code
cp SKILL.md ~/.claude/skills/web-analyzer/SKILL.md

# OpenClaw
cp SKILL.md ~/.openclaw/skills/web-analyzer/SKILL.md
```

## Usage

Once installed, simply provide a URL:

```
> analyze https://github.com/trending
```

Or multiple URLs:

```
> analyze the following sites:
> https://example.com
> https://news.ycombinator.com
> https://stripe.com
```

## Example Output

```markdown
## Site Analysis: https://example.com

### Tech Stack
- Framework: Next.js 15
- Libraries: React 19, Tailwind CSS 4.0
- CDN / Hosting: Vercel Edge Network

### SEO Audit
| Signal           | Status | Detail                    |
|------------------|--------|---------------------------|
| Title            | ✅     | "Example — Build Better"  |
| Meta Description | ✅     | 155 chars, keyword-rich   |
| Open Graph       | ✅     | Full og:image, og:title   |
| Canonical        | ✅     | Self-referencing           |
| Structured Data  | ✅     | JSON-LD Organization       |

### Accessibility
- Alt text coverage: 94% (2 images missing)
- ARIA usage: Extensive (nav, main, footer landmarks)
- Heading hierarchy: Clean (h1 → h2 → h3)

### Content Summary
- Word count: 1,247
- Key topics: developer tools, API platform, documentation
- Internal links: 23 / External links: 5
```

## JS Deep Analysis

Most modern websites are JS-heavy (React, Vue, Next.js, etc.) — static HTML analysis alone misses the real tech stack. The bundled `analyze.js` script solves this by running page JavaScript in a sandboxed Node.js context:

```bash
node analyze.js https://example.com --deep
```

This will:
- Extract all `<script>` blocks from the page
- Detect frameworks via runtime fingerprints (not just static patterns)
- Intercept `fetch()` and `XMLHttpRequest` calls to discover API endpoints
- Resolve dynamic configurations (env-based routing, feature flags)
- Verify discovered endpoints are live

The `--deep` flag enables dynamic JS evaluation. Without it, only static regex-based analysis is performed.

### Example

```bash
$ node analyze.js https://app.example.com --deep
{
  "url": "https://app.example.com",
  "frameworks": ["React", "Next.js"],
  "endpoints": [
    "https://api.example.com/v1/users",
    "https://api.example.com/v1/config"
  ],
  "endpointStatus": [
    { "url": "https://api.example.com/v1/users", "status": 200, "live": true },
    { "url": "https://api.example.com/v1/config", "status": 403, "live": false }
  ]
}
```

## Requirements

- Claude Code or OpenClaw CLI
- Node.js 18+ (for `analyze.js` deep analysis)

## License

MIT
