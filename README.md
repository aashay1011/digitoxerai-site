# DigiToxer — multi-variant landing site

Three positionings of the **same app**, one domain, switchable in seconds, ₹0/month.

```
/p/ally/       Adult accountability — a friend holds the key
/p/aspirant/   Exam prep and deep study — earn the scroll
/p/guardian/   Parent and child — screen time they earn
/_redirects    which variant answers at the bare domain
/netlify.toml  publish dir + security headers
```

## Deploy (once, ~10 minutes)

1. Push this folder to a GitHub repo.
2. Netlify → Add new site → Import from GitHub → pick the repo.
   Build command: *(leave empty)* · Publish directory: `.`
3. Netlify → Domain management → add `digitoxerai.app`, follow the DNS steps
   at your registrar. Netlify issues the HTTPS certificate automatically.

Free tier covers this entirely: hosting, HTTPS, custom domain, and 100 form
submissions a month.

## Switching which variant is live

Edit `_redirects`, leave exactly one line uncommented, commit. Live in about
20 seconds. Nobody sees a variant name in the URL bar — the rewrite is
invisible, which is what keeps the test honest.

All three stay reachable at their own paths at all times, whichever one is at
the root. That is how you run them side by side.

## Reading the results

Every form posts to the same `waitlist` form with a hidden `variant` field, so
Netlify → Forms shows one table with a variant column. That column is the whole
decision dataset.

Signups alone mean nothing without traffic. Add **Cloudflare Web Analytics**
(free, cookieless, no consent banner needed) — one script tag before `</body>`
on all three pages. The number that decides the pivot:

> unique visitors → email signups, **per variant, from the same traffic source**

Above 10% is strong. Below 5% means the positioning is wrong, not the traffic.

## How to run the test properly

Do not split traffic randomly — you don't have the volume for significance.
Post to each variant's own community, linking to that variant's own path:

| Variant | Where you post |
|---|---|
| `/p/ally/` | Recovery, quit-porn, quit-gambling, sobriety communities |
| `/p/aspirant/` | Exam-prep subreddits, Telegram study groups, study YouTubers |
| `/p/guardian/` | Parenting groups, school WhatsApp groups |

You are testing message-to-community fit, not layout. ~200 visitors per variant
is enough to see an obvious winner.

## Editing rules

- Each page is one self-contained HTML file. No build step, no framework.
- Keep the hidden `variant` value matching the folder name or the data is junk.
- Keep the honesty in the FAQs. The "can I just uninstall it?" answers are
  accurate to what Google Play actually permits, and getting caught overclaiming
  costs more than the conversions it buys.
- Adding a fourth variant: copy a folder, change the hidden `variant` value,
  add a commented line to `_redirects`.
