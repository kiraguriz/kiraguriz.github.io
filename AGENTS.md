# AGENTS.md

Project rules for any AI agent working in this repository. Read this file first.

## What this repo is

Static personal portfolio published as a GitHub user site at `kiraguriz.github.io`. Six HTML pages, one CSS file, one image folder. No JavaScript, no build step, no package manager, no framework.

Entry points:
- `index.html` - homepage with hero, signal grid, project grid
- `resume.html` - public resume (phone number intentionally omitted)
- `case-studies/*.html` - one page per project
- `assets/css/styles.css` - the only stylesheet
- `404.html`, `sitemap.xml`, `robots.txt`, `.nojekyll`

## Hard rules

Do not do any of the following without explicit approval from the owner:

- Do not introduce a build toolchain (npm, Vite, Webpack, Tailwind, Jekyll, etc.)
- Do not add analytics, tracking pixels, or third-party scripts of any kind
- Do not commit a real phone number anywhere on the site
- Do not modify `.nojekyll` (it is required to bypass Jekyll on GitHub Pages)
- Do not commit images that are not referenced by any HTML file
- Do not auto-commit or push. The owner controls publishing

## House style

- Color tokens live at the top of `assets/css/styles.css`. Reuse `--ink`, `--muted`, `--paper`, `--surface`, `--line`, `--sage`, `--rust` before defining new ones
- Typography is Inter plus system fallback. Headings use `clamp()` for fluid sizing
- Voice: first-person, concrete, technical. No marketing language. Match the tone of the hero copy in `index.html`
- Class naming is kebab-case, semantic, no utility classes
- Indent: two spaces, HTML and CSS

## Adding a new case study

1. Copy an existing file in `case-studies/` as a template (e.g. `vbird.html`)
2. Update `<title>`, `<meta name="description">`, and the OG meta block
3. Header nav must match the canonical nav (Work, Resume, GitHub, LinkedIn, Email)
4. Add the project card to the `.project-grid` in `index.html`
5. Append the new URL to `sitemap.xml` with a `<lastmod>` date
6. Optimize any new image (see Image rules) before committing
7. Verify in a browser at 360px, 760px, and 1280px widths

## Accessibility checklist

Run through this every time HTML changes:

- Every `<img>` has a descriptive `alt` attribute
- Every `<section>` that needs a label uses `aria-labelledby` pointing to a real heading id
- Heading order is sequential (no skipping h1 to h3)
- Skip-link at the top of `<body>` still works
- Keyboard tab order is logical, focus styles are visible
- Color contrast meets WCAG AA (`--muted` is only used on `--surface` or `--paper`, not on dark backgrounds)

## Image rules

- Convert new images to WebP. Keep PNG only if transparency or sharp UI screenshots demand it
- Target sizes: app icons under 100KB, content photos under 200KB, hero or OG images under 300KB
- Every `<img>` tag must include explicit `width` and `height` attributes to prevent layout shift
- Add `loading="lazy"` to images below the fold (anything past the hero)
- Provide a meaningful `alt`. Decorative-only images get `alt=""`, never omit the attribute

## SEO and metadata

Every page must have:

- `<title>` ending in `- Haitian Zhu`
- `<meta name="description">` under 160 characters
- `<meta property="og:title">`, `og:description`, `og:image`, `og:type`, `og:url`
- `<meta name="twitter:card" content="summary_large_image">`
- `<link rel="canonical">` to the absolute URL
- Favicon link

If a page is added or removed, update `sitemap.xml` in the same commit.

## Verification before declaring done

For any change that touches a page, do all of these:

1. Serve locally: `python3 -m http.server 8000` from the repo root, open every changed page
2. Visually inspect at three widths: 360px (mobile), 760px (tablet), 1280px (desktop)
3. Click every internal link on changed pages, confirm no 404
4. Validate HTML if structure changed: <https://validator.w3.org/nu/>
5. Run Lighthouse on the changed page. Targets: Performance >= 90, Accessibility = 100, Best Practices >= 95, SEO >= 95
6. If meta tags changed, paste the URL into a Twitter/LinkedIn card validator

State which of these you ran in your final message. Do not claim "done" without running them.

## Things to flag, not silently fix

If you notice any of these while doing other work, mention them to the owner, do not fix them as part of an unrelated change:

- Dead CSS tokens or rules
- Orphan image files
- Inconsistent navigation between pages
- Outdated dates in resume or case studies
- Broken external links

## Local preview

```sh
python3 -m http.server 8000
open http://localhost:8000
```

No live reload, no watcher, refresh manually.
