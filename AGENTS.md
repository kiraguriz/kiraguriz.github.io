# Portfolio site instructions

Goal: maintain a fast, accessible, evidence-backed static portfolio without introducing a build/runtime stack. Root `AGENTS.md` and `CLAUDE.md` are mirrors.

## Repository contract

- Hand-written HTML plus `assets/css/styles.css`; no build system or framework.
- `index.html` owns the homepage and `#resume`; `resume.html` is a noindex compatibility redirect. Case studies live under `case-studies/`.
- Everything committed outside ignored paths is publishable and crawlable. Do not commit scratch pages, local notes, review reports, mockups, private contact data, or unreferenced assets.

## Product and visual boundaries

- Reuse current `--studio-*` tokens, Charter/system serif body typography, and the self-hosted JetBrains Mono subset. Preserve the older token set only for legacy surfaces that still use it.
- Voice is first-person, concrete, technical, and tied to visible evidence; do not inflate claims.
- Inline vanilla JavaScript is progressive enhancement. Pages remain usable without JavaScript and preserve semantic HTML, focus visibility, sequential headings, skip links, keyboard order, and WCAG AA contrast.
- Do not add npm, bundlers, Jekyll, frameworks, analytics, third-party scripts/fonts, tracking, or auto-publish without explicit owner approval. Do not modify `.nojekyll`.

## Cross-page changes

- A case-study change updates title/description, social metadata, canonical URL, favicon, canonical navigation, `aria-current`, homepage work list, and `sitemap.xml` where applicable.
- Reference only optimized assets with explicit dimensions, useful alt text, and below-fold lazy loading.
- Keep responsive navigation and no-refresh homepage section behavior intact.

## Verification and publication boundary

Serve locally with `python3 -m http.server 8000`. Inspect every changed page in a real browser at relevant mobile/tablet/desktop widths and test changed links/navigation. Run HTML, Lighthouse, or social-card validation only when the changed concern requires it.

Done means changed pages render and navigate correctly, metadata/indexes agree, and all claims/assets are intentional. Do not commit, push, or publish unless explicitly requested.
