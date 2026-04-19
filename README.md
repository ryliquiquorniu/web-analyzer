# Web Analyzer

Instant website analysis for Claude Code and OpenClaw. Get tech stack detection, SEO audit, accessibility check, and content summary in one command.

## Features

- **Tech Stack Detection** — Identify frameworks, libraries, CDNs, and hosting from HTML fingerprints
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

## Requirements

- Claude Code or OpenClaw CLI
- No additional dependencies

## License

MIT
