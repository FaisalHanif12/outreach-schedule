# Local business web-development leads — tracker (Task 3)

Tracker, suppression list and rotation lists for the 10:00 Karachi routine (`0 5 * * *` UTC).

Migrated from the old document store on 17 August 2026. Rows unchanged. **Append rows now — you
have git.** Count before, append, count after, commit. Never reproduce the whole file.

Same respect rules as founder outreach: **one business gets ONE first touch, ever. Never invent an
email address or a phone number.**

---

## The two categories, and why they use different channels

**Category A — the business HAS a website. 7 per day. EMAIL.**
Audit the site, name three true specific problems, offer improvements, link one preview page
**only if the run fetched the URL and got HTTP 200.**

**Category B — the business has NO website. 3 per day. PHONE, NOT EMAIL.**

Verified 13 August 2026 across 30 targeted calls: **there is no free source that publishes an
email address for a US small business without a website.** Every high-volume directory holding
both the business and its email treats that email as its product and substitutes a relay form —
ChamberMaster uses `DirectoryEmailForm.aspx`, BBB uses its own contact form, Craigslist uses a
reply relay. Three chambers across two platforms yielded zero addresses. The only source that
published real ones was a hand-maintained farmers-market page with no index behind it and roughly
20 percent coverage.

So Category B is a **call list**. A phone call to a barber or a plumber converts better than cold
email anyway. The preview page is built for these leads too, so Faisal can send it the moment they
ask for something.

**Do not attempt to email a Category B business. Do not use a relay form. Do not send automated
SMS** — US TCPA rules on automated texting are far stricter than on email.

## Geography priority

United States first (the search tool is US-only, so yield is best there), then United Kingdom,
Australia, and EU/EEA.

## The sending cap — THE DOMAIN IS SHARED WITH TASK 1

`faisal@faisalhanif.work` sends both the founder outreach and these. **Gmail reputation is per
domain, not per task.** Task 3 runs at 10:00, after Task 1 at 08:00, so it can count what already
exists:

```
ceiling = min(7, 40 - drafts already created today)
```

**The number is 40, not 30.** An earlier version used 30, which produces zero drafts on every full
day, silently.

Category B leads are calls and count against **nothing**.

**Drafts do not warm a domain. Only sent mail does.** If drafts pile up unsent, do not advance any
ramp.

## Trade rotation

Rotate daily so the same neighbourhood is not mined twice. **Record the pairing in the report**
and do not reuse a pairing from the last seven days.

barber · hair salon · coffee shop · cafe · restaurant · dentist · chiropractor · gym · yoga studio
· plumber · electrician · HVAC · landscaping · auto repair · pet grooming · florist · bakery ·
tattoo studio · nail salon · physiotherapy · roofing · cleaning service · driving school ·
photography studio · med spa

## City rotation (US-first)

Asheville NC · Boise ID · Chattanooga TN · Des Moines IA · Fort Collins CO · Greenville SC ·
Knoxville TN · Lancaster PA · Madison WI · Missoula MT · Ogden UT · Portland ME · Reno NV ·
Roanoke VA · Savannah GA · Sioux Falls SD · Spokane WA · Springfield MO · Tallahassee FL ·
Wichita KS · Wilmington NC · Boulder CO · Bend OR · Charleston SC · Fargo ND

**Mid-size cities deliberately.** Large metros are already saturated with agencies cold-emailing
these businesses; mid-size markets have far less competition for attention.

## The list

| business_domain | business | city | state | category | contact | email_or_phone | source_url | date_added | status |
|---|---|---|---|---|---|---|---|---|---|
| carvingrock.kitchen | Carving Rock Kitchen | Chattanooga | TN | A | shop inbox | carvingrockkitchen@gmail.com | https://www.carvingrock.kitchen/ | 2026-08-14 | drafted |
| goodmancoffeeroasters.com | Goodman Coffee Roasters | Chattanooga | TN | A | shop inbox | goodmancoffeeroasters@gmail.com | https://www.goodmancoffeeroasters.com/ | 2026-08-14 | drafted |
| federalbakeshop.com | Federal Bake Shop | Hixson (greater Chattanooga) | TN | A | shop inbox | info@federalbakeshop.com | https://federalbakeshop.com/contact-us/ | 2026-08-14 | drafted |
| butterthebread.com | Bread and Butter | Chattanooga | TN | A | shop inbox | contact@butterthebread.com | https://butterthebread.com/contact-1 | 2026-08-14 | drafted |
| terry-brown-plumbing-253062 | Terry Brown Plumbing | Knoxville | TN | B | owner name not published | (865) 256-3374 | https://www.yellowpages.com/knoxville-tn/mip/terry-brown-plumbing-253062 | 2026-08-14 | queued |
| smith-cleaning-service-462492076 | Smith Cleaning Service | Knoxville | TN | B | Christina, Owner | (865) 386-3191 | https://www.yellowpages.com/knoxville-tn/mip/smith-cleaning-service-462492076 | 2026-08-14 | queued |
| kc-lawn-service-510952206 | Kc Lawn Service | Knoxville | TN | B | owner name not published | (865) 247-4379 | https://www.yellowpages.com/knoxville-tn/mip/kc-lawn-service-510952206 | 2026-08-14 | queued |

**Status values:** `queued` · `drafted` · `called` · `sent` · `REPLIED` · `BOUNCED` · `OPTOUT` ·
`rejected`.

**Only `queued` and `drafted` permit future contact, and only when EVERY comma-separated token of
the status cell is one of those two.** An ALL test, never a CONTAINS test.

For Category B rows, `business_domain` is the profile URL slug, since there is no domain. (These
three carry YellowPages slugs rather than BBB, per the 14 August note below. Same purpose, still a
stable unique key.)

**Note on the four Category A rows above:** all four hold emails linking to preview pages that
were never uploaded, so the links 404. They are recorded as contacted and will not be written to
again. See the repo README for what to do about them.

## Sources, with verified status

| Source | Status | Use |
|---|---|---|
| WebSearch (trade + city) | **WORKS**, US-only | Primary Category A discovery |
| The business's own website | **WORKS** | The audit, and where the published email is found |
| BBB profiles (bbb.org) | **DEAD as of 14 August — `PROVENANCE_REQUIRED` on every URL** | Was the primary Category B source. See below. **Do not spend calls on it.** |
| YellowPages `/mip/` profiles | **WORKS**, with two traps | Replacement Category B source: phone, address, years in business, sometimes an owner name |
| manta.com | **WORKS** | Best free source for an owner name and year established. **Underused** |
| Google Maps | DEAD | A JavaScript shell, and a Business Profile has no email field at all |
| Chamber directories | Mostly dead | Relay forms, JS shells, or robots-blocked. Varies per chamber |
| Yelp, Facebook, Instagram | `ROBOTS_DISALLOWED` | Out |
| Yell, TripAdvisor | Readable, zero emails | Not useful for email |
| Craigslist services | Readable, relay only | Right businesses, unusable contact |
| Apify Google Maps actor | Only when Faisal's laptop is open | Optional. Note it reads emails from the business **website**, not from Maps, so it helps Category A only |

## 14 August 2026 — BBB is gone, and what replaced it

**`bbb.org` is unreachable from the run environment.** Three separate URLs across two agents: the
Cooper's Plumbing profile named in the old prompt, an Asheville barber-shop category page, and BBB
links surfaced in search. Every one returned `error_type: PROVENANCE_REQUIRED` — "The permission
request for this URL was not answered in time."

**Nobody is present on a scheduled run to answer a permission prompt, so this is permanent for
unattended runs, not a transient failure.** WebFetch itself was healthy throughout and read dozens
of other sites in the same run.

**The replacement, and its two traps.**

1. **The YP category-listing page reports "Website: Yes" for every business on it.** Template text
   being misread. Flatly wrong — returned for all 30 businesses across two Knoxville categories.
   **Never trust it. Open the individual profile.**
2. **`*.localsearch.com` is a YellowPages auto-generated microsite, not a real website.** YP
   creates one free for every listing, so a genuinely tiny operator usually shows a website link
   despite never having built anything. Proof it is machine-generated: the subdomain embeds the YP
   listing ID from the profile URL — `karenskleaningservice464428578.localsearch.com` against YP
   listing `464428578`. (These pages were never directly readable, so this is structural evidence
   rather than direct inspection.)

**Consequence.** "No website link on the YP profile" is a much stricter test than BBB's explicit
blank field was, and it **under-counts badly**. The localsearch tier **is** the real target pool
for Category B. Treat `*.localsearch.com` as equivalent to no website, say so in the packet, and
confirm on the call — which costs nothing, since there is no sender reputation at stake on a phone
channel.

## Grading Category B evidence

Because the no-website test is weaker now, every Category B row carries a grade:

- **Grade 1** — no website link on the profile at all, **and** a name search returned no own-domain
  site. Strongest available.
- **Grade 2** — the only website link is a `*.localsearch.com` auto-microsite, **and** a name
  search returned no own-domain site. Still a real lead; open the call by confirming it, which is
  a natural question anyway.
- **Not a lead** — an own domain was found anywhere, or the profile could not be read.

**An UNREADABLE profile is never filed as a rejection.** Different outcomes, separate tallies.

## Preview pages

Every lead in **both** categories gets a self-contained HTML preview page using their real business
name, real services and the specific problems found. Committed to `previews/<date>/` in this repo
and delivered with `SendUserFile`.

**The email carries ONE link, never an attachment** — attachments on cold email are a serious spam
signal, stronger than links.

Hosting is manual: Faisal uploads to `https://faisalhanif.work/p/<slug>`. **The run fetches that
exact URL and requires HTTP 200 before the link goes in the email.** No 200, no link — the
sentence becomes an offer to send the concept instead.

That is a mechanism, not a warning, and the difference is the whole point. The old version of this
file said the packet "must say in capitals that the files have to be uploaded BEFORE the drafts are
sent". It did say so, in capitals. Four businesses still received emails with dead links.
