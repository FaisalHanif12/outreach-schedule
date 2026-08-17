# previews/ — the concept pages, and the link in the email

Task 3 commits its generated HTML here, one folder per run date:

```
previews/2026-08-18/oakleaf-barbers.html
previews/2026-08-18/goodman-coffee-roasters.html
```

One self-contained file per lead, **both categories**. The no-website call leads get one too, so
Faisal can send it the moment somebody asks to see something.

**Read this file before writing the first page of a run.**

---

## Why the page carries the pitch and the email does not

A cold email from a stranger gets about four seconds. It cannot hold a redesign proposal, and any
email that tries reads as a mailshot and goes to spam.

So the split is: **the email proves you looked. The page proves you can build.** Three true
findings and one sentence about what they cost the business is enough to earn a click. Everything
else lives on the page.

That is also why the page has to be genuinely good. It is not an attachment, it is an audition.

---

## The two page types

### Type A — the business already has a website

Structure: **what I found → what it costs them → what it looks like fixed.**

1. **One line of context.** Their business name, their trade, their city, and that you looked at
   their site. Nothing else.
2. **The three findings, each with its evidence.** The URL you fetched, the exact text you read,
   or the element that was absent and how you proved it was absent. **No adjectives.** State the
   fact and let them check it.
3. **The fix, shown rather than described.** This is the part that matters.
   - Finding is "no way to book online" → build a **working mobile booking form** on the page.
     Real service names taken from their site, real prices if they publish them, a date and time
     picker they can actually tap through.
   - Finding is "menu is a photograph" → lay their **actual menu** out as readable HTML, with
     their real items and prices.
   - Finding is "booking widget points at a vendor page that no longer loads" → show the working
     path end to end.
   - Finding is "no way to request a quote" → build the quote form, with the fields that trade
     actually needs.
4. **An honest close.** What is a quick fix, what is a bigger piece of work. Naming the bigger
   piece as bigger is what makes the quick part believable.

**A page that says "we would add online booking" is a proposal. A page where they can press the
button is a demonstration.** Everyone sends proposals.

### Type B — the business has no website

These are the phone leads. The page is what Faisal sends the moment one of them asks to see
something, so it answers *"what would a website actually do for me?"* — not *"here is a website."*

1. **Them, laid out the way a customer would want to find them.** Real name, trade, city, phone,
   address, opening hours, years in business. All from the directory profile you opened.
2. **The two or three systems that matter for that specific trade**, built as working examples:
   - barber, salon, tattoo, med spa → online booking with real service names and durations
   - cafe, bakery, restaurant → menu, ordering, directions, hours
   - plumber, electrician, HVAC, roofer → emergency call-out, service area map, licence display,
     quote request
   - cleaner, landscaper, driving school → quote request and recurring booking
   - dentist, physiotherapist, chiropractor → appointment booking with first-visit intake
3. **A short line on what it would take to build.** Plain, no pricing.

---

## Build rules — both types

**Self-contained.** Inline CSS, no external stylesheets, no frameworks, no CDN links, no fonts
fetched over the network. JavaScript only where a demonstration genuinely needs it, inline.
**The file must render correctly with no network at all** — a business owner may well open it on
a phone with bad signal, and a page that half-loads has proved the wrong thing.

**Mobile-first.** Design at 375px wide and let it grow. Most of these people will open it on a
phone, and for Type A the argument is frequently that their current site does not work on one.

**Real content only.**

| Never | Instead |
|---|---|
| Stock photography | No photography. Type, space and colour |
| An invented logo for their business | Their name set in type |
| Fake testimonials or review counts | Nothing, or their real published reviews quoted with the source |
| Invented statistics, percentages, revenue or traffic figures | Describe the mechanism, never the magnitude |
| Countdown timers, "limited slots", urgency devices | A plain sentence |
| Lorem ipsum anywhere | Their real services, or leave the section out |

**Restrained.** One accent colour, generous whitespace, a readable type scale, no animation beyond
a hover state. Small businesses distrust flashy, and flashy is what every template agency sends.
Restraint reads as competence.

**Fast and small.** Under about 100KB. No embedded images unless they are inline SVG.

**Footer, exactly:** `Concept prepared by Faisal Hanif - faisalhanif.work`

---

## What makes it credible rather than salesy

Five things, in order of how much they matter.

**1. Evidence next to every claim.** "Your booking button links to `bookings.example.com/xyz`,
which returns a 404" beats "your booking is broken" by a distance, because they can check it in
ten seconds and the checking is what builds trust. Every finding on the page should be falsifiable
by them in under a minute.

**2. Nothing invented.** One made-up number destroys the other nine true things on the page.
A business owner who catches a single fabricated statistic assumes the rest is fabricated too, and
they are being reasonable.

**3. Working over described.** A form they can tap is proof of competence. A bullet list of
"features we can add" is a brochure.

**4. Naming the limits.** "The booking flow here is a working front end. Wiring it to your
calendar and taking deposits is a bigger piece of work" is more persuasive than implying it is all
finished. Overclaiming is the tell of someone who has not built it before.

**5. It is about their business, not about web design.** They do not care about your grid system.
They care that nobody can book at nine in the evening.

---

## Hosting — how the link gets live

The email carries the link **only if the run fetched that exact URL and got HTTP 200.** No 200,
no link — the sentence changes to an offer to send the concept instead. That is a mechanism, not a
warning, and it exists because on 14 August four real businesses received emails pointing at pages
that had been generated but never uploaded. Every link 404'd. The risk had been written down in
advance and guarded with a capitalised note. **That was not enough.**

So on any morning the pages are not live yet, every email ships link-free. Correct behaviour. The
packet lists which slugs need uploading.

### The three ways to make them live

**Option A — manual upload to `faisalhanif.work/p/<slug>`.** What the system assumes today.
Faisal downloads the day's HTML from the run and uploads it. Best-looking URL, most credible
domain, but it is a manual step every morning and if he is busy the whole day ships link-free.

**Option B — GitHub Pages off this repo.** Turn Pages on for `main`, and every file the routine
commits to `previews/` is live within a minute of the commit. **Fully automatic — the run's own
commit publishes the page, so the link check passes on the same morning without Faisal touching
anything.** Add a `CNAME` file with a subdomain like `p.faisalhanif.work` and a DNS CNAME record,
and the URLs read as his own domain rather than `github.io`.

> **The catch, and it decides this:** GitHub Pages publishes **everything in the repo**, and this
> repo contains `state/do-not-contact.md`. Turning Pages on here would put 257 people's names and
> email addresses on a public URL. **Do not enable Pages on this repository as it stands.** Either
> move the previews to their own separate repository, or move `state/` out of the repository
> entirely first.

**Option C — a second repository, previews only.** A public `faisal-previews` repo with Pages on
and a custom domain, holding nothing but HTML concept pages. Clean separation: the outreach repo
stays private, the concept pages are public and instantly live. The cost is that the routine
cannot push to a second repository on its own, so publishing stays a manual step unless a small
GitHub Action mirrors `previews/` across.

**The recommendation is C**, and it is worth the twenty minutes of setup: it removes the manual
morning upload from the critical path, and the pages are meant to be publicly reachable anyway —
that is what a link in an email means.

### What must never be public

Whatever hosting is chosen: the concept pages are public by design, but nothing else is.
`state/do-not-contact.md` and `state/local-business-leads.md` hold real people's names, email
addresses and phone numbers. Those never sit behind a public URL, on Pages or anywhere else.
