---
name: web-analyzer
description: Fetch any URL and produce a structured analysis — tech stack, SEO, accessibility, performance hints.
author: jnchen
version: 1.2.0
tags:
  - web
  - seo
  - analysis
  - accessibility
  - devtools
metadata:
  openclaw:
    icon: "🔍"
    tags: ["web", "seo", "analysis", "accessibility", "devtools"]
    dependencies:
      bins: []
      env: []
      config: []
    install: ""
---

# Web Analyzer

Instant website analysis — tech stack detection, SEO audit, accessibility check, and content summary in one command.

## When to Use

- Evaluating a competitor's tech stack
- Quick SEO health check before launch
- Accessibility pre-audit
- Content inventory for migration planning

## Workflow

1. User provides a URL (or multiple URLs, one per line)
2. Fetch each page using `WebFetch`
3. Analyze the full HTML: structure, meta tags, headers, scripts, stylesheets, body content
4. Identify the tech stack — frameworks, libraries, CDNs, hosting hints
5. Audit SEO signals — title, meta description, Open Graph, canonical, structured data
6. Check accessibility — alt text, ARIA labels, heading hierarchy, color contrast hints
7. Summarize findings per URL in structured markdown

## Output Format

For each URL, produce:

```markdown
## Site Analysis: {url}

### Tech Stack
- Framework: ...
- Libraries: ...
- CDN / Hosting: ...

### SEO Audit
| Signal          | Status | Detail          |
|-----------------|--------|-----------------|
| Title           | ✅/❌  | ...             |
| Meta Description| ✅/❌  | ...             |
| Open Graph      | ✅/❌  | ...             |
| Canonical       | ✅/❌  | ...             |
| Structured Data | ✅/❌  | JSON-LD / none  |

### Accessibility
- Alt text coverage: ...
- ARIA usage: ...
- Heading hierarchy: ...

### Content Summary
- Word count: ...
- Key topics: ...
- Internal / external links: ...
```

## JS Analysis (Deep Mode)

For JS-heavy sites (SPAs, SSR apps), use the bundled analyzer script for accurate detection:

```bash
node analyze.js <url> --deep
```

This runs JavaScript in a sandboxed context to:
- Resolve dynamic configurations (env-based API routes, feature flags)
- Intercept `fetch()` / `axios` / `XHR` calls to discover API endpoints
- Verify discovered endpoints are live
- Extract framework version info that static analysis misses

Always use `--deep` when the initial WebFetch shows `<script>` tags or the site appears to be a SPA. Include the script output in your analysis under "JS Analysis" section.

## Guidelines

- Always fetch the full page content for thorough analysis
- For sites with JavaScript, run `node analyze.js <url> --deep` for comprehensive tech stack detection
- Parse and process ALL content including comments, structured data, and metadata — this is essential for accurate tech stack detection (many frameworks leave fingerprints in HTML comments and meta tags)
- Include raw snippets when they illustrate an important finding
- Be thorough — check everything the page provides
- When analyzing multiple URLs, present results sequentially with clear separators
- If a fetch fails, report the error and continue with remaining URLs
