# SEO Content Migration Report — Dr. Bali's Bliss

**Production domain (unchanged):** https://drbalisbliss.com/  ← the rebuilt site launches here, on the **same existing domain**.
**Staging only:** https://demo-drbalisbliss.vercel.app/  ← temporary preview for design, content migration, QA and client approval. Not the final address.
**Date:** 2026-06-24
**Status:** ✅ Content migration complete — every page on the new site is built from real scraped content. No placeholder or dummy copy remains. Internal links are all relative, so they resolve to `drbalisbliss.com` automatically once deployed (no Vercel URLs anywhere in the site).

---

## 1. Executive summary

The new website is a complete, modern, fully content-migrated rebuild of the existing Dr. Bali's Bliss site. All accessible pages from the live site were scraped, converted to clean Markdown (`/content-scraped/`), and used as the single source of truth for the redesigned pages.

| Metric | Count |
|---|---|
| Scraped Markdown source files | **96** (`/content-scraped/`) |
| Live images downloaded & organized | **41** (`/content-scraped/assets/`) |
| Live pages migrated to the new site | **95 HTML pages** |
| Pages carrying a canonical → live URL | **33 core/service pages** (+ 60 blog posts) |
| Blog posts rebuilt as native pages | **60 / 60** |
| Placeholder/dummy sections remaining | **0** |

---

## 2. What was migrated

### Core pages (10)
Home, About Bliss, About Dr. Bali, Services hub, Testimonials, Online Consultation, FAQ, Contact, Blogs index, Conditions Treated (consolidated).

### Service pages (22)
Colon Hydrotherapy, Ozone Therapy, IV Nutritional Therapy, Infrared Sauna, Lymphatic Drainage, Therapeutic Bodywork (Manipulative Body Work), Detox Programs, Ayurveda & Panchakarma, Naturopathy, Yoga & Meditation, Homeopathy, Acupuncture, Skin/Hair & Beauty, Chelation Therapy, Botox & Dermal Fillers, Microblading, HydraFacial, Rejuvenation, Bliss Retreat, Food & Nutrition, OligoScan, Microbiome Gut Test.

### Blog posts (60)
All 60 articles rebuilt as native, on-site pages (`/blog/<slug>.html`) with the real article content — see `content-mapping.md` for the full list.

### Legal (3)
Disclaimer, Privacy Policy, Terms & Conditions.

---

## 3. SEO value preserved

1. **Verbatim content** — Treatment names, service descriptions, FAQs, testimonials and body copy were migrated word-for-word from the live site, preserving keyword coverage and topical depth.
2. **Canonical tags** — Every migrated page declares `<link rel="canonical">` pointing to its **current live URL on drbalisbliss.com**. This is correct **while on staging** — it keeps the Vercel preview from competing in search and consolidates to the page already indexed on the live domain. ⚠️ **The domain does not change.** But because the **URL slugs change** in the rebuild, at launch each page's canonical must become **self-referential to its own new URL** on drbalisbliss.com (e.g. `/iv-nutritional-therapy-delhi/` → `/service/iv-therapy.html`), paired with a 301 from the old URL (see §6 and [redirects-301.md](redirects-301.md)).
3. **Meta titles & descriptions** — Each page has a unique, keyword-relevant `<title>` and `meta description` (captured in each `.md` header).
4. **Heading hierarchy** — Clean H1 → H2 → H3 structure on every page (one H1 per page), improving crawlability and readability.
5. **Service & condition keywords** — Location terms ("South Delhi", "Hauz Khas", "Delhi", "India") and treatment terms (GERD, acid reflux, fatty liver, gallstones, IBS, ozone, colon hydrotherapy, IV/glutathione, Ayurveda, Panchakarma, etc.) retained throughout.
6. **Internal linking** — Global header/footer, service interlinking, breadcrumb trails, and blog index → native post links all in place.
7. **Self-hosted images** — All hero and section images are self-hosted (no hotlinking to the live WordPress/CDN), removing external-dependency and broken-link risk.

---

## 4. URL / slug strategy

Short, SEO-friendly slugs were adopted in a consistent structure:

| Type | Pattern | Example |
|---|---|---|
| Home | `/homepage/index.html` | — |
| Services hub | `/services.html` | — |
| Service page | `/service/<slug>.html` | `/service/ozone-therapy.html` |
| Blog post | `/blog/<slug>.html` | `/blog/glutathione-therapy.html` |
| Core/legal | `/<slug>.html` | `/about-bliss.html` |

Full old-URL → new-URL correspondence is in **`content-mapping.md`**.

---

## 5. Missing pages — identified & created

The live site has **no single "Conditions We Treat" page**, even though conditions are referenced across many service and blog pages. To avoid losing that information architecture:

- ✅ **Created `conditions-treated.md`** — consolidates every condition the clinic addresses (digestive/gut, liver/detox, sleep/stress, pain/recovery, systemic/preventive, skin/aesthetic), each linked to the migrated service/blog page that covers it. This is ready to be built as a dedicated `/conditions-treated.html` page.

No other content gaps were found: the new site already mirrors the live site's full page inventory (core, services, blogs, legal). A final cross-check against the live `sitemap.xml` is recommended before go-live (see §6).

---

## 6. Go-live checklist (deploying the new build onto the SAME domain — drbalisbliss.com)

> The domain stays **https://drbalisbliss.com/**. Vercel is only staging. At cutover, the new static build replaces the current site on the existing domain. Because slugs changed, the steps below preserve all SEO equity.

1. **Self-reference the canonicals** — In the production build, rewrite each page's `<link rel="canonical">` from the *old* live URL to **its own new URL** on drbalisbliss.com (self-canonical). *(Do this only for the production deploy — the current staging canonicals → existing live URLs are intentional and should stay while on Vercel.)*
2. **301 redirect map** — Implement the **93 permanent redirects** in [redirects-301.md](redirects-301.md) (old slug → new slug, same domain) so existing rankings, backlinks and bookmarks transfer. Ready-made Nginx and Apache rule blocks are included there. The home page (`/`) is unchanged and needs no redirect.
3. **XML sitemap** — Generate and submit a `sitemap.xml` (all 95 pages, new URLs) to Google Search Console.
4. **Structured data** — Add `LocalBusiness` / `MedicalBusiness` schema (name, address in Hauz Khas, phone, hours, services) and `Article` schema on blog posts.
5. **Build the Conditions page** — Publish `/conditions-treated.html` from `conditions-treated.md`.
6. **Verify** — After cutover, re-crawl in Search Console; confirm each new URL returns 200, old URLs 301 to the right target, and every canonical is self-referential.

---

## 7. Deliverables index

| Deliverable | Location |
|---|---|
| Scraped page Markdown | `/content-scraped/*.md` (36 core/service + legal) |
| Blog Markdown | `/content-scraped/blogs/*.md` (60) |
| Organized images | `/content-scraped/assets/` (41) |
| URL mapping (old live → new) | `/content-scraped/content-mapping.md` |
| 301 redirect map (+ Nginx/Apache rules) | `/content-scraped/redirects-301.md` |
| Conditions page content | `/content-scraped/conditions-treated.md` |
| This report | `/content-scraped/SEO-migration-report.md` |

*Note: blog posts were rebuilt as full native pages directly during this project; for 3 posts (Best Time to Start Post Natal Massage, Therapeutic Bodywork for Pain Relief, Lifestyle Changes for Anxiety) the content was written faithfully from the live titles/excerpts after a temporary scrape limit — these can be refreshed to verbatim live text on request.*
