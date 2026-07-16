# answerhouse-tools

Static tools and lead assets for Answerhouse Advisory, served at **tools.answerhouseadvisory.com** via GitHub Pages.

No build step. No framework. Plain HTML, CSS and vanilla JS. What's committed is what's live.

---

## Live URLs

| URL | File | Notes |
| --- | --- | --- |
| `tools.answerhouseadvisory.com` | `index.html` | M&A Internal Communications Readiness Assessment. **This is the URL to promote.** |
| `tools.answerhouseadvisory.com/confirmed` | `confirmed/index.html` | Double opt-in landing page. Set as the confirmation redirect in MailerLite. Not promoted, `noindex`. |
| `tools.answerhouseadvisory.com/readiness-assessment` | `readiness-assessment.html` | Redirect stub to root. Preserves an older published link. Do not promote. |

`CNAME` binds the custom domain. **Never delete or edit it.**

---

## Naming convention for new assets

**Folder with an `index.html` inside. Always.**

| Wanted URL | File to create |
| --- | --- |
| `/faq` | `faq/index.html` |
| `/day-one-checklist` | `day-one-checklist/index.html` |
| `/manager-scripts` | `manager-scripts/index.html` |

Never `faq.html`. That produces `/faq.html` in the address bar, which is what the redirect stub above exists to clean up.

**Rules:**

- **Lowercase only.** GitHub Pages is case-sensitive. `/FAQ` and `/faq` are different URLs and one of them 404s.
- **Hyphens, not underscores or spaces.** Spaces become `%20`. Underscores disappear under link underlines.
- **Short.** Two or three words. These get pasted into LinkedIn comments and emails.
- **Name the thing, not the format or the audience.** `/five-questions`, not `/five-questions-pdf-for-ceos`.
- **No dates or version numbers.** `/faq-2026` is wrong by January. Version the content, not the URL.

**Non-page files keep their extension** and live in one place:

```
/downloads/five-questions.pdf
```

For a gated asset, build a page at `/five-questions` that handles the gate and links the file in `/downloads`. Promote the page, not the file.

---

## The one permanent rule

**Never rename a published URL.**

Once a link is in a LinkedIn comment, an email or a deck, it's a commitment. If a URL has to move, leave a redirect stub at the old path. `readiness-assessment.html` is the working template for this.

---

## Design system

Every page shares one system. Copy an existing page rather than starting fresh.

**Colors** (declared as CSS custom properties in `:root`)

| Token | Hex | Role |
| --- | --- | --- |
| `--navy` | `#0B2C4B` | Structure. Headers, CTA blocks, headings. |
| `--copper` | `#C7573A` | Action only. Buttons, focus rings, the rule under the header. |
| `--plum` | `#9C2F6C` | Orientation. Eyebrows, progress fill, aside rules. **Very sparingly.** Two or three uses per page maximum. |
| `--gray` | `#E5E7EB` | Warm gray. |
| `--white` | `#FFFFFF` | |

Derived tokens (`--ink`, `--muted`, `--muted-lt`, `--hairline`, `--canvas`, `--copper-dk`) are defined in each page's `:root`. Keep them consistent.

**Type:** Montserrat only, weights 300 to 700, loaded from Google Fonts. Inter is retired. Body 17px, negative letter-spacing on headings, uppercase tracked labels at 11 to 13px.

**Shape:** 3px radius. 1px hairline borders. No drop shadows. No gradients. Left-aligned.

**Layout:** 920px container. Two-column grids so the right column carries content rather than white space. Breakpoints at 880px and 640px.

---

## Known debt

The design system is duplicated in each page's `<style>` block. Fine at two pages. **Before adding a third or fourth, extract it to `/assets/answerhouse.css`** and link it from every page. Otherwise a color change lands in one file and silently misses the others.

---

## Deploy and test

1. Commit. GitHub Pages rebuilds in a minute or two.
2. **Test in incognito.** A normal browser serves a cached copy and makes working changes look broken.
3. When adding a page and a redirect together, commit the new page first and confirm it loads. A redirect pointing at a 404 takes down the working URL.

---

## Lives outside this repo

- **MailerLite** owns the assessment's email gate. The form endpoint is hardcoded in `index.html`. The form record controls double opt-in, groups, the confirmation email and the confirmation redirect. The form's own design is unused, since the markup here is hand-written. **Don't re-embed MailerLite's snippet over it.**
- **Cal.com** owns Clarity Call scheduling. Booking links are hardcoded.
- **Cloudflare** owns DNS, plus SPF, DKIM and DMARC for email authentication.
- **Carrd** owns answerhouseadvisory.com, including the Privacy Policy anchor that `index.html` links to. **If that anchor changes, the consent block link breaks silently.**

---
