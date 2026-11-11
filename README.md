# Soorsi Barrierefrei

Event website for "Soorsi Barrierefrei - Dini Idee bewegt!", built with Jekyll and editable through [Pages CMS](https://pagescms.org).

## Content editing

All texts and images are edited in Pages CMS (schema in `.pages.yml`):

- **Konfiguration** (`_data/site.yml`): site title, Google description, registration e-mail, logo, default share image, Google Search Console verification code, optional banner with link, UI texts (menu, skip link)
- **Fusszeile** (`_data/footer.yml`): contact heading and text, e-mail on/off, links (Impressum, social media, ...), copyright text
- **Startseite** (`index.html` front matter): hero, structured event data for search engines (date, place, organizer, free, status), "Google & Teilen" overrides, intro, info boxes, registration (e-mail or external form link), directions, extra sections and their position. Every block has an "Abschnitt anzeigen" switch.
- **Weitere Seiten** (`_seiten/*.md`, Jekyll collection `seiten`, URL `/<filename>/`): title, menu position/label, intro, image, sections, "Google & Teilen" incl. noindex. Every published page appears in the main menu automatically (`_includes/nav.html`); `published: false` keeps a draft out of the build, menu and sitemap. `_seiten/ueber-uns.md` is such a draft with placeholder texts.
- **Fehlerseite** (`404.html` front matter)

Content files intentionally contain only front matter; the markup lives in `_includes/page-*.html`. The free sections ("Weitere Abschnitte": text, optional image above/left/right, background, button) are rendered by `_includes/sections.html` on both the home page and the extra pages. Links typed into the CMS go through `_includes/url.html`, which adds the baseurl to site-internal paths. Layouts are assigned in `_config.yml`, not in front matter, so the CMS cannot remove them.

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

To also check draft pages (menu, sitemap, links), build with drafts:

```bash
bundle exec jekyll build --unpublished && script/images && TEST_UNPUBLISHED=1 script/test
```

`script/images` writes the downscaled hero image copies used in the `srcset` (ImageMagick, or `sips` on macOS). `script/test` runs html-proofer (internal links, images, alt texts) and checks that the event data from the CMS files reaches the rendered page, that every page has one `<h1>`, a skip link and a canonical link (or noindex), that extra pages appear in the menu and the sitemap while drafts stay unpublished, plus the SEO output: canonical link, Open Graph image, schema.org Event JSON-LD, `robots.txt` and `sitemap.xml`.

## Deployment

Every push to `main` builds, tests and publishes the site to GitHub Pages (`.github/workflows/deploy.yml`). In the repository settings, set Pages > Source to "GitHub Actions".

The flyer source files (`fllyer_barrierefrei_v5 Ordner/`, zip) are not part of the repository.
