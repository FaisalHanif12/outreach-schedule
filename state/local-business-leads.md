# Local business web-development leads — tracker (Task 3)

Tracker, suppression list and rotation lists for the 10:00 Karachi routine (`0 5 * * *` UTC).

Migrated from the old document store on 17 August 2026. Rows unchanged. **Append rows now — you
have git.** Count before, append, count after, commit. Never reproduce the whole file.

Same respect rules as founder outreach: **one business gets ONE first touch, ever. Never invent an
email address or a phone number.**

---

## The two categories, and why they use different channels

**Category A — the business HAS a website. 15 per day, floor 10. EMAIL.**
Audit the site, name three true specific problems, say in one line what they cost the business,
offer the improvement, and link one preview page **only if the run fetched the URL and got HTTP
200.** Raised from 7 to 15 on 17 August, and spread across five regions rather than US-only.

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

## Geography — five regions, roughly three leads each

Set by Faisal on 17 August. **United States · United Kingdom · Canada · Australia · EU/EEA.**
Record the split in every report.

WebSearch is US-weighted, so expect one or two extra calls per non-US lead. That is budgeted for
and is not a reason to quietly fall back to US-only.

- **UK, Ireland, Canada and Australia** are the easiest non-US pools. English-language sites, and
  small businesses publish a contact address at roughly the same rate as in the US.
- **EU sites in other languages are in scope and are frequently the best leads**, because almost
  nobody is cold-emailing them in English about their booking flow. German, Austrian and Dutch
  sites carry an `Impressum` or `Contact` page with a real published address as a legal
  requirement, which makes address verification easier there than anywhere else.
- **Write every email in English.** A machine-translated cold email reads worse than a plain
  English one, and getting a language subtly wrong is a stronger negative signal than writing in
  the wrong language on purpose.

**Category B (no website) stays US-only.** The replacement source is YellowPages `/mip/` profiles,
which is a US directory. Equivalent non-US directories have not been tested from the run
environment, and an untested source producing three phone numbers a day is not worth the calls
until someone checks it.

## The sending cap — THE DOMAIN IS SHARED WITH TASK 1

`faisal@faisalhanif.work` sends both the founder outreach and these. **Gmail reputation is per
domain, not per task.** Task 3 runs at 10:00, after Task 1 at 08:00, so it can count what already
exists:

```
ceiling = min(15, 40 - drafts already created today)
```

**The number is 40, not 30.** An earlier version used 30, which produces zero drafts on every full
day, silently.

**There is no headroom left.** Task 1 takes up to 25, Task 3 up to 15, so a full day is exactly
40 against a 40-per-day maximum. Before 17 August it was 20 + 7 = 27, with thirteen spare. The
subtraction in that formula is therefore mandatory, not defensive: if Task 1 over-ran, Task 3
absorbs it.

Category B leads are calls and count against **nothing**.

**Both routines print a deliverability block every run** — bounces in the last 24 hours, bounce
rate, replies. Above 2 percent bounce, the report opens in capitals recommending a volume pause.
Historically every bounce in this campaign came from a shared inbox and no personal published
address has ever bounced, so a spike usually means address quality slipped rather than the domain
being burnt. The run says which it looks like; Faisal decides what to do about it.

**Drafts do not warm a domain. Only sent mail does.** If drafts pile up unsent, do not advance any
ramp.

## Trade rotation

Rotate daily so the same neighbourhood is not mined twice. **Record the pairing in the report**
and do not reuse a pairing from the last seven days.

barber · hair salon · coffee shop · cafe · restaurant · dentist · chiropractor · gym · yoga studio
· plumber · electrician · HVAC · landscaping · auto repair · pet grooming · florist · bakery ·
tattoo studio · nail salon · physiotherapy · roofing · cleaning service · driving school ·
photography studio · med spa

## City rotation — mid-size markets in all five regions

**Mid-size cities deliberately, everywhere.** Large metros are already saturated with agencies
cold-emailing these businesses; mid-size markets have far less competition for attention. Never
use London, New York, Toronto, Sydney or Berlin.

**United States**
Asheville NC · Boise ID · Chattanooga TN · Des Moines IA · Fort Collins CO · Greenville SC ·
Knoxville TN · Lancaster PA · Madison WI · Missoula MT · Ogden UT · Portland ME · Reno NV ·
Roanoke VA · Savannah GA · Sioux Falls SD · Spokane WA · Springfield MO · Tallahassee FL ·
Wichita KS · Wilmington NC · Boulder CO · Bend OR · Charleston SC · Fargo ND

**United Kingdom and Ireland**
Bath · Bristol · Cambridge · Cheltenham · Chester · Derby · Exeter · Harrogate · Ipswich ·
Lancaster · Norwich · Oxford · Perth (Scotland) · Plymouth · Shrewsbury · Stirling · Swansea ·
Truro · Winchester · York · Cork · Galway · Kilkenny · Limerick · Waterford

**Canada**
Barrie ON · Guelph ON · Halifax NS · Hamilton ON · Kelowna BC · Kingston ON · Kitchener ON ·
Lethbridge AB · London ON · Moncton NB · Nanaimo BC · Red Deer AB · Regina SK · Saskatoon SK ·
Sherbrooke QC · St. Catharines ON · Sudbury ON · Thunder Bay ON · Trois-Rivieres QC ·
Victoria BC · Waterloo ON · Whitby ON · Windsor ON · Kamloops BC · Charlottetown PE

**Australia and New Zealand**
Ballarat VIC · Bendigo VIC · Cairns QLD · Coffs Harbour NSW · Darwin NT · Geelong VIC ·
Hobart TAS · Launceston TAS · Mackay QLD · Newcastle NSW · Rockhampton QLD · Toowoomba QLD ·
Townsville QLD · Wagga Wagga NSW · Wollongong NSW · Bunbury WA · Albury NSW · Dubbo NSW ·
Hamilton NZ · Tauranga NZ · Dunedin NZ · Napier NZ · Palmerston North NZ · Nelson NZ ·
Queenstown NZ

**EU and EEA**
Ghent BE · Bruges BE · Leuven BE · Groningen NL · Eindhoven NL · Haarlem NL · Maastricht NL ·
Aarhus DK · Odense DK · Bergen NO · Trondheim NO · Uppsala SE · Malmo SE · Tampere FI ·
Turku FI · Graz AT · Salzburg AT · Innsbruck AT · Freiburg DE · Heidelberg DE · Munster DE ·
Regensburg DE · Porto PT · Coimbra PT · Girona ES · San Sebastian ES · Bologna IT · Verona IT

**Note on the EU block:** an `Impressum` page is legally required in Germany and Austria and
almost always carries a real published email address. Start there when the EU slot is proving
hard to fill.

## Netlify deploy state — the run reads and updates this line

```
netlify_pages_deployed: 0 (never)
```

**This is the anti-wipe guard and it is load-bearing.** A Netlify zip deploy replaces the entire
site, so a run that assembles only today's pages would erase every previously published concept
page — including URLs sitting in emails already sent. Before deploying, the run counts what it is
about to upload and compares it to this number. Greater: deploy. **Equal or lower: refuse**, ship
every email link-free, and say so in capitals. After a successful deploy it rewrites this line.

`0 (never)` means nothing has been published yet, so the first deploy always proceeds.

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
| foxbarber.com | Fox Barber and Beauty | Asheville | NC | A | shop inbox | see-gmail-draft-2026-08-17 | reconstructed from draft | 2026-08-17 | drafted |
| saltypawz910.com | Salty Pawz | not recorded | US | A | shop inbox | see-gmail-draft-2026-08-17 | reconstructed from draft | 2026-08-17 | drafted |
| ritualyogamissoula.com | Ritual Yoga Missoula | Missoula | MT | A | shop inbox | see-gmail-draft-2026-08-17 | reconstructed from draft | 2026-08-17 | drafted |
| physio-norwich | Norfolk Physiotherapy and Acupuncture Clinic | Norwich | UK | A | clinic inbox | see-gmail-draft-2026-08-17 | reconstructed from draft, DOMAIN TRUNCATED | 2026-08-17 | drafted |
| uniqueinkyork.co.uk | Unique Ink York | York | UK | A | studio inbox | see-gmail-draft-2026-08-17 | reconstructed from draft | 2026-08-17 | drafted |
| colinhawkins.co.uk | Colin Hawkins Photography | not recorded | UK | A | Colin | see-gmail-draft-2026-08-17 | reconstructed from draft | 2026-08-17 | drafted |
| frontenacchiropractic.com | Frontenac Chiropractic | Kingston | ON | A | clinic inbox | see-gmail-draft-2026-08-17 | reconstructed from draft | 2026-08-17 | drafted |
| motorcitymechanics.ca | Motor City Mechanics | not recorded | CA | A | shop inbox | see-gmail-draft-2026-08-17 | reconstructed from draft | 2026-08-17 | drafted |
| toowoombadental.com.au | Toowoomba Dental | Toowoomba | QLD | A | practice inbox | see-gmail-draft-2026-08-17 | reconstructed from draft | 2026-08-17 | drafted |
| eastendhub.com.au | East End Hub | not recorded | AU | A | shop inbox | see-gmail-draft-2026-08-17 | reconstructed from draft | 2026-08-17 | drafted |
| chanecoiffures.nl | Chane Coiffures | not recorded | NL | A | salon inbox | see-gmail-draft-2026-08-17 | reconstructed from draft | 2026-08-17 | drafted |
| fysiotherapieheezerweg.nl | Fysiotherapie Heezerweg | Eindhoven | NL | A | practice inbox | info@fysiotherapieheezerweg.nl | reconstructed from draft | 2026-08-17 | drafted |
| handy-services-by-chris | Handy Services by Chris | Greenville | SC | B | not recorded | see packet 2026-08-17 | reconstructed from preview slug | 2026-08-17 | queued |
| premiere-maintenance | Premiere Maintenance | Greenville | SC | B | not recorded | see packet 2026-08-17 | reconstructed from preview slug | 2026-08-17 | queued |
| commercial-industrial-plumbing | Commercial Industrial Plumbing | Greenville | SC | B | not recorded | see packet 2026-08-17 | reconstructed from preview slug | 2026-08-17 | queued |

**Status values:** `queued` · `drafted` · `called` · `sent` · `REPLIED` · `BOUNCED` · `OPTOUT` ·
`rejected`.

*** EVERY ROW ABOVE BLOCKS. THERE IS NO STATUS THAT MAKES A BUSINESS SOURCEABLE AGAIN. ***

A row exists here because that business is already in the pipeline. `drafted` means a draft is
waiting in Gmail for Faisal to press Send. `queued` means it is on the call list. Both are contacts
about to happen, and re-sourcing either produces a second first touch.

Status decides what may still happen to a row already here — whether Faisal may call it, whether it
is finished — **not whether it can be discovered again. It cannot.** That test is an ALL test over
every comma-separated token, never a CONTAINS test: `sent, REPLIED` is closed, not open.

For Category B rows, `business_domain` is the profile URL slug, since there is no domain. (These
three carry YellowPages slugs rather than BBB, per the 14 August note below. Same purpose, still a
stable unique key.)

**Note on the four Category A rows above:** all four hold emails linking to preview pages that
were never uploaded, so the links 404. They are recorded as contacted and will not be written to
again. See the repo README for what to do about them.


## RECONSTRUCTED ROWS — 18 August, read this before doubting them

The 17 August run appended 15 rows here (7 to 22) and **could not push them**. It sent the updated
file to Faisal directly, but that file was never put back into the repo, so as of this morning the
tracker still held the original 7 rows — meaning **tomorrow's run would have re-contacted all
twelve businesses it drafted yesterday.**

The 15 rows above were therefore reconstructed by hand from the Gmail drafts and the preview page
filenames. **They are a safety net, not the authoritative record.**

**What they do correctly:** blocking is keyed on `business_domain`, and every domain above was read
verbatim off a real draft. All twelve website leads and all three call leads are now blocked.
That is the job these rows exist to do and they do it.

**What they do not have:** exact email addresses (only Fysiotherapie Heezerweg's was visible),
source URLs, three cities, the Category B phone numbers and owner names, and the per-lead findings.

**Two things to fix when convenient, neither urgent:**

1. **If the 22-row `local-business-leads.md` that Task 3 sent on 17 August is still available,
   use it instead of these rows.** It is the real record. These were rebuilt from a screenshot.
2. **`physio-norwich` is a truncated domain.** It was cut off in the source and the TLD is unknown,
   so it is recorded as read rather than guessed. It will not block a `physio-norwich.co.uk`
   candidate by exact match. Correct it from the draft when you next open Gmail.

## Sources, with verified status

| Source | Status | Use |
|---|---|---|
| WebSearch (trade + city) | **WORKS**, US-weighted but returns non-US results | Primary Category A discovery, all five regions |
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
name, real services and the specific problems found. **Committed to `previews/<date>/` in this
repo — that commit is the delivery mechanism.** Build rules are in `previews/README.md`.

**The email carries ONE link, never an attachment** — attachments on cold email are a serious spam
signal, stronger than links.

**Hosting is automatic as of 18 August.** The run deploys every concept page to Netlify, served at
`<SITE_URL>/<slug>`, before drafting a single email. **It then fetches that exact
URL and requires HTTP 200 before the link goes in the email.** No 200, no link — the
sentence becomes an offer to send the concept instead.

That is a mechanism, not a warning, and the difference is the whole point. The old version of this
file said the packet "must say in capitals that the files have to be uploaded BEFORE the drafts are
sent". It did say so, in capitals. Four businesses still received emails with dead links.
