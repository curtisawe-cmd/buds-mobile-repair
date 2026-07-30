# Bud's Mobile Repair LLC - Website

Single-page marketing site for a mobile auto-repair business. Static HTML, no build
step, no dependencies. Open `index.html` in a browser to preview; that is the whole
dev loop.

Repo: https://github.com/curtisawe-cmd/buds-mobile-repair (remote `origin`, branch `main`)

## Layout

| Path | Tracked | What it is |
| --- | --- | --- |
| `index.html` | yes | The entire site. Markup, CSS, and JS are all inline in this one file. |
| `bmr-logo.png` | yes | The approved logo. Used in header, hero, footer, and as the favicon. |
| `.gitignore` | yes | Keeps source art, scratch renders, and print assets out of the repo. |
| `card.html` | no | Business card artwork for print (3.5x2in, front and back). Ignored on purpose. |
| `Buds-Mobile-Repair-Business-Card.pdf` | no | Rendered card for the printer. |
| `logo.png`, `*.HEIC`, `BMR Logo (approved).png` | no | Source art. Do not commit; `bmr-logo.png` is the only logo the site needs. |

Only three files are tracked. If a new asset is needed on the live site, confirm it
is not caught by an existing `.gitignore` rule before committing.

## Business facts

These appear in many places across `index.html` and `card.html`. Change them
everywhere or not at all.

- Phone: (315) 690-0731, linked as `tel:+13156900731`
- Email: budsmobilerepair@gmail.com
- Hours: Mon-Fri 9AM to 6PM, Sat 8AM to 1PM (described as "6 days a week")
- Service area: Wayne & Monroe counties, NY
- Experience: 23+ years
- Services: Diagnostics, Brakes & Suspension, Batteries & Electrical, Oil &
  Maintenance, Small Engine Repair

## Copy conventions

**No em dashes, en dashes, or non-breaking hyphens anywhere in user-facing copy.**
This has been cleaned up twice already (`fb59ae5`, `83684c7`) and is easy to
reintroduce by accident. Use a comma, a period, or the word "to" instead. Ranges are
written "Mon-Fri 9AM to 6PM" with a plain ASCII hyphen. The middot `·` is fine and is
used deliberately as a separator.

Headings are uppercase Oswald; body copy is Inter. Both load from Google Fonts.

## Brand colors

Defined as CSS variables in `:root` at the top of `index.html` and mirrored in
`card.html`. The blues are matched to the logo lettering.

```
--bg:#0e0f12   --panel:#16181d   --panel-2:#1d2027
--steel:#2a2e37   --line:#31353f
--text:#e9eaed   --muted:#9aa0ac
--amber:#4b3bf0   (indigo, the primary accent)
--amber-2:#0c0970 (navy, used for gradients and heading drop-shadows)
```

The `--amber` / `--amber-2` names are historical. The palette was switched from amber
to blue in `cc34127` and the variable names were left alone, so **amber means blue**.
Renaming them would touch a lot of lines for no visual gain.

Headings get a two-tone effect via `text-shadow:0.05em 0.06em 0 var(--amber-2)`, which
puts a navy shadow under the indigo, echoing the logo.

## Two integration points

Both are configured by editing a single JS variable near the bottom of `index.html`.
Each is written so that an empty string degrades gracefully instead of breaking.

### Booking calendar - LIVE

`BOOKING_URL` (around line 609) holds a Google Calendar appointment-schedule URL with
`?gv=true` on the end. On load, a script swaps the "call to book" fallback card for an
iframe pointing at it. Set it back to `""` and the fallback card returns.

### Quote form - NOT LIVE

`FORM_ENDPOINT` (around line 630) is still `""`, so the form runs in demo mode: it
shows a confirmation message and resets, but **sends nothing**. The AJAX submit path is
already written and tested-shaped; it only needs the endpoint.

To go live: create a free form at formspree.io pointed at budsmobilerepair@gmail.com,
then paste the `https://formspree.io/f/xxxxxxx` endpoint into that variable. Once set,
the handler POSTs a `FormData`, shows a real success message, and falls back to an
alert telling the customer to call if the request fails.

## Conventions worth keeping

- Everything inline in `index.html`. No splitting into separate CSS/JS files unless
  there is a real reason.
- Mobile matters more than desktop here. Customers find this on a phone. There is a
  sticky call bar fixed to the bottom below 720px, and breakpoints at 960 / 720 / 520 /
  360px.
- Phone numbers are always `tel:` links so a tap dials.
- Commit messages are short and describe the user-visible change.
