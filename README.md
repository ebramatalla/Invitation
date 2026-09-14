# دعوة زفاف أبرام ودنيا — Digital Wedding Invitation

Single-page, static, RTL Arabic wedding invitation. Plain HTML/CSS/JS — no
framework, no build step, no backend, no localStorage.

## Files

```
index.html        Everything: markup, CSS, and JS inline in one file
imgs/README.txt   Notes on the two asset files you need to add
```

## Files you need to add yourself

Nothing pulls images from the internet — these are referenced by path but
**not included**. The site works fine without them (see below), but add them
before sharing the link widely:

| File               | Purpose                                              | Required? |
|--------------------|-------------------------------------------------------|-----------|
| `imgs/og-image.jpg`| 1200×630 image shown when the link is shared (WhatsApp, Facebook, Twitter previews) | Recommended |
| `imgs/sound.mp3`   | Background music, starts after "افتح الدعوة" is tapped | Optional — if missing, the floating music button auto-hides and nothing breaks |

## Values you need to edit before publishing

All of these are marked with `TODO` comments in `index.html`:

1. **Domain / site URL** — appears in three places:
   - `<meta property="og:url">` and `<meta property="og:image">` (head)
   - `<meta name="twitter:image">` (head)
   - `CONFIG.siteUrl` in the `<script>` at the bottom (used by the share button)

   Replace `https://REPLACE-WITH-YOUR-DOMAIN.vercel.app/` with your real
   Vercel URL once you know it (or your custom domain).

2. **Ceremony & reception times** — currently placeholders (`18:00` /
   `20:00`). Edit `CONFIG.ceremonyTime` and `CONFIG.receptionTime` in the
   `<script>` block, and update the matching visible text in the schedule
   cards (search for `TODO: وقت الكنيسة` and `TODO: وقت الاستقبال` in the
   HTML). The countdown and the "Add to calendar" button both read from
   `CONFIG`, so updating it there keeps everything in sync.

3. **Map links** — already filled in with the links you provided
   (`CONFIG.ceremonyMapLink`, `CONFIG.receptionMapLink`); only touch these if
   a venue changes.

## Deploying to Vercel

No build step is needed — this is a static site.

**Option A — Vercel dashboard**
1. Push this folder to a GitHub/GitLab/Bitbucket repo (or use Vercel's
   "drag and drop" deploy at https://vercel.com/new).
2. Import the repo in Vercel.
3. Framework preset: choose **Other** (or leave auto-detected as static).
   Build command and output directory can stay empty/default — Vercel serves
   `index.html` as-is.
4. Deploy. Vercel gives you a `*.vercel.app` URL.
5. Go back into `index.html` and replace `REPLACE-WITH-YOUR-DOMAIN` with
   that URL (or your custom domain), then redeploy.

**Option B — Vercel CLI**
```bash
npm i -g vercel
vercel        # first deploy, follow the prompts
vercel --prod # promote to production
```

## Notes on how it behaves

- **Audio autoplay**: browsers block audio until a user gesture. Music only
  starts after the visitor taps "افتح الدعوة" on the opening screen, which
  satisfies that requirement.
- **Missing `sound.mp3`**: the `<audio>` element's `error` event hides the
  floating music button entirely, so no broken UI is shown.
- **Reduced motion**: scroll fade-ins are skipped (content shows immediately)
  when the visitor's OS has "reduce motion" enabled.
- **Share button**: uses `navigator.share` on supporting mobile browsers;
  falls back to copying the link to the clipboard (with a small toast) on
  desktop browsers that don't support the Web Share API.
