# دعوة زفاف أبرام ودنيا — نسخة الكنيسة فقط

Church-ceremony-only variant of the wedding invitation. Same page/design as
the full invite, but with the reception section removed — for guests invited
to the church ceremony only. Plain HTML/CSS/JS, no framework, no build step,
no backend, no localStorage.

## Files

```
index.html        Everything: markup, CSS, and JS inline in one file
imgs/README.txt   Notes on the two asset files you need to add
```

## Files you need to add yourself

| File               | Purpose                                              | Required? |
|--------------------|-------------------------------------------------------|-----------|
| `imgs/og-image.jpg`| 1200×630 image shown when the link is shared (WhatsApp, Facebook, Twitter previews) | Recommended |
| `imgs/sound.mp3`   | Background music, starts after "افتح الدعوة" is tapped | Optional — auto-hides the music button if missing |

`imgs/sound.mp3` was copied over from the main invite project, so it should
already work. Replace it if you want different music for this variant.

## What's different from the full invite

- The "برنامج اليوم" schedule section now shows only the ceremony card
  (church venue, time, map link) — the reception card was removed.
- `CONFIG` in the `<script>` block no longer has `receptionTime`,
  `receptionVenue`, or `receptionMapLink` — only ceremony fields remain.
- The "أضف إلى التقويم" (add to calendar) button only references the
  ceremony — it no longer mentions the reception in the event details.
- Page `<title>` is "دعوة زفاف أبرام ودنيا — مراسم الإكليل" to distinguish
  it from the full invite when both are open in tabs/bookmarks.

Everything else (splash screen, hero with parents' names, verse, countdown,
share button, design) is identical to the main invite.

## Values you need to edit before publishing

Same as the main invite — all marked with `TODO` comments in `index.html`:

1. **Domain / site URL** — in the `og:url`, `og:image`, `twitter:image` meta
   tags and in `CONFIG.siteUrl` (used by the share button).
2. **Ceremony time** — `CONFIG.ceremonyTime` in the `<script>` block, and the
   matching visible text in the schedule card (search for
   `TODO: وقت الكنيسة`).
3. **Map link** — `CONFIG.ceremonyMapLink`, already filled in; only touch if
   the venue changes.

## Deploying to Vercel

Same as the main invite — no build step needed.

**Vercel dashboard**: push this folder to a Git repo, import it in Vercel,
framework preset "Other" (static), deploy, then go back and replace
`REPLACE-WITH-YOUR-DOMAIN` with the real URL you get.

**Vercel CLI**:
```bash
npm i -g vercel
vercel        # first deploy, follow the prompts
vercel --prod # promote to production
```

This is a separate project from the main invite — deploy it under its own
Vercel project (its own domain/URL) so the two links stay distinct for the
two different guest lists.
