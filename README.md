# SecureShare — static site

A production-ready, multi-page static site for SecureShare: private file and text
sharing protected by one-time-password (OTP) verification and automatic expiration.

## Contents

```
secureshare-site/
  index.html          Home
  features.html       /features
  security.html       /security
  faq.html            /faq
  contact.html        /contact
  privacy.html        /privacy
  terms.html          /terms
  404.html            custom not-found page
  robots.txt          crawl rules + sitemap reference
  sitemap.xml         all indexable URLs
  llms.txt            summary for LLM crawlers
  assets/
    styles.css        shared stylesheet
    site.js           shared, minified JavaScript
    favicon.svg       scalable favicon
    favicon-32.png    32x32 PNG favicon
    apple-touch-icon.png
    og-home.png       social share images (1200x630)
    og-features.png
    og-security.png
    og-faq.png
```

## Deploying

The site is plain HTML/CSS/JS — no build step. Upload the contents of
`secureshare-site/` to any static host.

- **Netlify / Vercel / Cloudflare Pages:** point the project at the folder. All three
  serve extensionless ("clean") URLs automatically, so `/features` resolves to
  `features.html`.
- **GitHub Pages:** push the folder to a repo and enable Pages. GitHub Pages also
  serves extensionless URLs.
- **Any web server:** configure a rewrite so extensionless paths map to the matching
  `.html` file, and route unknown paths to `404.html`.

### Custom domain

Canonical tags, `og:url` values, `sitemap.xml` and `robots.txt` all reference
`https://secureshare.app`. If the domain changes, find-and-replace
`secureshare.app` across the HTML files and the two text files.

### Local preview

Because the site uses clean root-relative URLs, open it through a local web server
rather than double-clicking the file:

```
cd secureshare-site
python3 -m http.server 8000
# then visit http://localhost:8000/
```

## SEO & metadata included

- Unique `<title>` and meta description on every page
- Canonical tag on every page
- Exactly one `<h1>` per page
- Open Graph + Twitter card tags with 1200x630 share images
- `sitemap.xml`, `robots.txt`, `llms.txt`
- Visible breadcrumbs on all inner pages
- JSON-LD structured data: `Organization`, `WebSite` and `SoftwareApplication` on the
  home page; `BreadcrumbList` on inner pages; `FAQPage` on the FAQ
- Favicon (SVG + PNG) and Apple touch icon
- `noindex` on the 404 page

## Notes on the original checklist

- **Vite / React tab title, source maps, JS bundles:** not applicable — this site has
  no framework or bundler. There is a single hand-written, minified `site.js`.
- **Local business schema:** deliberately not used. `LocalBusiness` markup describes a
  business with a physical location customers visit; for a web product the correct
  types are `Organization` + `SoftwareApplication`, which is what the home page uses.

## Before going live

- Review `privacy.html` and `terms.html` with a qualified professional; they are
  plain-language drafts, not legal advice.
- The contact page uses email addresses (support@, abuse@, security@, hello@) — make
  sure those mailboxes exist at the domain.
- The sharing panel on the home page is front-end only. Real uploads, OTP generation
  and verification, storage and expiry must run on a server.
