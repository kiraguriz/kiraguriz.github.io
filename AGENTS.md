# AGENTS.md

Project rules for any AI agent working in this repository. Read this file first.

## What this repo is

Static personal portfolio published as a GitHub user site at `kiraguriz.github.io`. Hand-written HTML and one CSS file. No build step, no package manager, no framework. A small amount of inline vanilla JS is allowed for progressive enhancement only (see below).

Pages:
- `index.html` - single-page homepage: hero, About, Now, Selected work, Resume, Postscript. The resume lives here as the `#resume` section
- `case-studies/*.html` - one page per project: `workout-movement-tracker`, `onlyplanes`, `vbird`, `poker`, `chicago-traffic`
- `resume.html` - thin redirect to `index.html#resume` (kept for old inbound links; `noindex`, not in the sitemap)
- `404.html`, `sitemap.xml`, `robots.txt`, `.nojekyll`
- `assets/css/styles.css` - the only stylesheet
- `assets/images/` - WebP/PNG assets; `assets/haitian-zhu-resume.pdf` - downloadable resume

## Hard rules

Do not do any of the following without explicit approval from the owner:

- Do not introduce a build toolchain (npm, Vite, Webpack, Tailwind, Jekyll, etc.)
- Do not add analytics, tracking pixels, or third-party scripts of any kind
- Inline JS is for progressive enhancement only (e.g. the nav pill in `index.html`, the case-study subnav centering). The page must work with JS disabled. Do not add JS dependencies, bundlers, or framework runtimes
- Do not commit a real phone number anywhere on the site
- Do not modify `.nojekyll` (it is required to bypass Jekyll on GitHub Pages)
- Do not commit images that are not referenced by any HTML or CSS file
- Do not commit dev artifacts, design scratch pages, or mockups to the published tree (they get deployed and crawled). Keep them out of the repo
- Do not auto-commit or push. The owner controls publishing

## House style

- Color tokens live in `:root` at the top of `assets/css/styles.css`. The active design system is the `--studio-*` set (`--studio-paper`, `--studio-ink`, `--studio-muted`, `--studio-line`, `--studio-surface`, `--studio-accent` violet `#4f3dcf`, etc.). Reuse these before defining new ones. An older non-studio token set (`--ink`, `--muted`, `--paper`, `--surface`, `--line`, `--sage`, `--rust`, `--blue`, `--gold`) is still used by `404.html`; leave it unless you are touching that page
- Typography: display and body are Charter (serif, system fallback Georgia/Palatino); labels and code use JetBrains Mono (loaded from Google Fonts). Fluid sizing via `clamp()`. Do not introduce Inter as a content font — the `:root` Inter declaration is only a base fallback that studio components override
- Voice: first-person, concrete, technical. No marketing language. Claims should match shown evidence — do not name projects in About/Now that have no case study or visible artifact. Match the tone of the hero copy in `index.html`
- Class naming is kebab-case, semantic, no utility classes. Site-wide chrome uses the `studio-` prefix; case-study pages use the `case-` prefix
- Indent: two spaces, HTML and CSS

## Adding a new case study

1. Copy an existing file in `case-studies/` as a template (e.g. `vbird.html`)
2. Update `<title>`, `<meta name="description">`, and the OG/Twitter meta block, plus `<link rel="canonical">`
3. Header nav must match the canonical nav: About, Now, Work, Resume (pointing at `../index.html#...`), plus GitHub, LinkedIn, and the "Open to opportunity" email pill
4. Update the case-study subnav pills in every sibling case-study page so the set stays in sync, and set `aria-current="page"` on the new page
5. Add the project row to `.studio-work-list` in `index.html`
6. Append the new URL to `sitemap.xml`
7. Optimize any new image (see Image rules) before committing
8. Verify in a browser at 360px, 760px, and 1280px widths

## Accessibility checklist

Run through this every time HTML changes:

- Every `<img>` has a descriptive `alt` attribute (decorative-only images get `alt=""`, never omit)
- Every `<section>` that needs a label uses `aria-labelledby` pointing to a real heading id
- Heading order is sequential (no skipping h1 to h3)
- Skip-link at the top of `<body>` still works
- Keyboard tab order is logical, focus styles are visible
- Color contrast meets WCAG AA (`--studio-muted` is only used on `--studio-paper`/`--studio-surface`, not on dark backgrounds)
- The page is usable with JavaScript disabled

## Image rules

- Convert new images to WebP. Keep PNG only if transparency or sharp UI screenshots demand it
- Target sizes: app icons under 100KB, content photos under 200KB, hero or OG images under 300KB
- Every `<img>` tag must include explicit `width` and `height` attributes to prevent layout shift
- Add `loading="lazy"` to images below the fold (anything past the hero)
- Provide a meaningful `alt`. Decorative-only images get `alt=""`, never omit the attribute
- OG images (`og:image`) must be PNG or JPG, referenced by absolute URL

## SEO and metadata

Every indexable page must have:

- `<title>` ending in `- Haitian Zhu`
- `<meta name="description">` under 160 characters
- `<meta property="og:title">`, `og:description`, `og:image`, `og:type`, `og:url`
- `<meta name="twitter:card" content="summary_large_image">`
- `<link rel="canonical">` to the absolute URL
- Favicon link

If a page is added or removed, update `sitemap.xml` in the same commit. Redirect/`noindex` pages (like `resume.html`) must stay out of the sitemap.

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
- Outdated dates in the resume, the "Now" section, or case studies
- Broken external links
- Mismatched cache-bust query strings on `styles.css` between pages

## Local preview

```sh
python3 -m http.server 8000
open http://localhost:8000
```

No live reload, no watcher, refresh manually.
