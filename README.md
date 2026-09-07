# Haitian Zhu Portfolio

Hand-written static GitHub Pages site. No build step or runtime dependencies.

## Local preview

```sh
python3 -m http.server 8000
```

Open http://127.0.0.1:8000/. The homepage and five case studies share `assets/css/styles.css`. Inline vanilla JavaScript enhances image inspection, email copying, and section navigation.

## Pages and compatibility

- `index.html` contains the work, about, contact, and resume content. Existing `#overview` and `#resume` links remain valid.
- Project pages retain their canonical `case-studies/` URLs, listed in `sitemap.xml`.
- `resume.html` redirects to the homepage resume section.

## Assets and checks

OnlyPlanes screenshots are archived iOS captures from July 22, 2026; the workout recording is an archived Android demo. Other project illustrations are identified in the page content. Arrow icons derive from Heroicons; see [the license](assets/HEROICONS-LICENSE.txt).

Before publication, check each page at desktop, tablet, and mobile widths, local links and fragments, metadata, keyboard navigation, and media. Publishing is a separate explicit action.
