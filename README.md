# Soorsi Barrierefrei

One-page event website for "Soorsi Barrierefrei - Dini Idee bewegt!", built with Jekyll and editable through [Pages CMS](https://pagescms.org).

## Content editing

All texts and images are edited in Pages CMS (schema in `.pages.yml`):

- **Konfiguration** (`_data/site.yml`): site title, description, registration e-mail, optional banner
- **Startseite** (`index.html` front matter): hero, structured event data for search engines (date, place), intro, info boxes, registration, directions, extra sections
- **Fehlerseite** (`404.html` front matter)

`index.html` and `404.html` intentionally contain only front matter; the markup lives in `_includes/page-*.html`. Layouts are assigned in `_config.yml`, not in front matter, so the CMS cannot remove them.

## Local development

Requires Ruby >= 3.1.

```bash
bundle install
bundle exec jekyll serve
```

## Tests

```bash
bundle exec jekyll build && script/images && script/test
```

`script/images` writes the downscaled hero image copies used in the `srcset` (ImageMagick, or `sips` on macOS). `script/test` runs html-proofer (internal links, images, alt texts) and checks that the event data from the CMS files reaches the rendered page, plus the SEO output: canonical link, Open Graph image, schema.org Event JSON-LD, `robots.txt` and `sitemap.xml`.

## Deployment

Every push to `main` builds, tests and publishes the site to GitHub Pages (`.github/workflows/deploy.yml`). In the repository settings, set Pages > Source to "GitHub Actions".

The flyer source files (`fllyer_barrierefrei_v5 Ordner/`, zip) are not part of the repository.
