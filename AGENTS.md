# AGENTS.md

This repository is a Hugo static site (theme: hugo-clarity). The `content/post/` Markdown files are blog posts.

## Image creation guidelines
- Thumbnails are configured via front matter `thumbnail` and must be square.
- Current site convention uses square images at `310x310` pixels.
- For line art (e.g., robot head), use a uniform stroke thickness of `10px`.
- Keep thumbnails simple and high-contrast (black on white preferred for this site).
- Place thumbnail assets under `static/images/` and reference them like `/images/<file>.png`.
- If a header image is needed, use `featureImage` (and optionally `featureImageAlt`) in front matter.

## Blog post header (front matter) contents
Typical front matter keys used in posts:
- `title`
- `date`
- `description`
- `thumbnail`
- `featureImage`
- `featureImageAlt`
- `tags`
- `categories`
- `draft`

## Markdown content rule
- Do **not** start the Markdown body of a blog post with a `#` heading. The first line after front matter should be regular text or a lower-level heading if needed.
