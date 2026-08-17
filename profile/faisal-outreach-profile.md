# Faisal — outreach profile

**Reference data only.** The two `ROUTINE-INSTRUCTIONS.md` files own the workflow, the filters,
the budgets and the daily targets. This file owns only the facts about Faisal and the fixed copy.
If this file and a routine file ever disagree, **the routine file wins** and the conflict gets
reported so this one can be corrected.

---

## Who this is

**M Faisal Hanif**, Software Engineer, Lahore, Pakistan (UTC+5, no daylight saving). Remote only.

| | |
|---|---|
| Outreach address | `faisal@faisalhanif.work` |
| Job-application address | `mehrfaisal111@gmail.com` — **different address, deliberately** |
| Phone | `+923148166354` |
| Portfolio | `https://faisalhanif.work` — **NO HYPHEN.** `faisal-hanif.work` is dead |
| LinkedIn | `https://www.linkedin.com/in/faisal-frontend-developer/` |
| GitHub | `https://github.com/FaisalHanif12` |
| X | `https://x.com/FaisalHanif333` |

3+ years experience, 10+ projects shipped, **2 companies** (Techxelo, Viral Square).
BS Software Engineering, University of Management and Technology (UMT), 2020–2024.

**Stack:** JavaScript, TypeScript, React, Next.js, Node, Express, React Native, Expo, Redux,
Tailwind, REST, GraphQL, JWT, MongoDB, PostgreSQL, MySQL, Firebase, Docker, CI/CD, AWS, system
design, LLM features via Gemini and OpenRouter.

**NOT in his stack — never claim these:** Go, Rust, Python, PHP, Java, C#, Kotlin, Swift, Vue,
Angular, Kubernetes, Terraform, Playwright, Puppeteer, Cypress.

## The sending address, and the one thing neither routine can control

Both routines draft from Gmail. **`create_draft` has no `from` parameter.** Drafts leave from
whatever Gmail has as the account's default sending address, which Faisal confirmed on
12 August 2026 is `faisal@faisalhanif.work`.

A routine can neither set nor verify this. So: **never attempt a workaround, and never put a
"From:" line in the body.** If the address is ever wrong, that is a Gmail settings change Faisal
makes himself.

**The job-application address stays `mehrfaisal111@gmail.com` and is never used for outreach, and
the outreach address is never put on a CV.** The Gmail has years of sending reputation; the
`faisalhanif.work` domain is new and its inbound depends on a forwarding service. A missed
interview invitation costs far more than a smarter-looking address gains.

## The domain sending ceiling — 40 per day, shared, and now fully used

Both routines draft from the same domain, and Gmail reputation is per domain, not per task.

```
Task 1 (08:00) takes up to 25.   target 25, floor 15
Task 3 (10:00) takes min(15, 40 - drafts already created today).   target 15, floor 10
```

**The number is 40, not 30.** An earlier version used 30, which produces zero Task 3 drafts on
every full day, silently. If the arithmetic comes out at zero or less, Task 3 creates no email
drafts, says so plainly, and still delivers its three call leads, which count against nothing.

### What changed on 17 August, and the risk that came with it

Faisal raised the targets from 20 and 7 to **25 and 15**. That is 40 exactly, against a
40-per-day maximum. Before, it was 27 with thirteen spare.

**This was his call, made knowing the trade, and the routines implement it. But the risk is real
and is written here so nobody has to rediscover it:**

`faisalhanif.work` was first used for sending in August 2026. It has been doing roughly 11 to 30
a day. Going to a hard 40 every day, on cold outreach, from a domain that young, is the profile
that gets mail quietly filtered rather than bounced — and quietly is the problem, because nothing
in the pipeline can see a spam-folder placement.

Two things follow, and both are now mandatory in the routine files rather than advisory:

1. **The subtraction in Task 3's formula is not optional.** If Task 1 over-ran, Task 3 absorbs it.
   Neither task may exceed its own number for any reason.
2. **Both routines print a deliverability block every run** — bounces in the last 24 hours, the
   bounce rate, and replies. **Above 2 percent bounce, the report opens in capitals recommending a
   volume pause.** The run never changes the target itself; that stays Faisal's decision. It just
   makes the number impossible to miss.

The useful baseline: **every bounce this campaign has ever produced came from a shared inbox, and
no personal address published for a named person has ever bounced.** So a bounce spike almost
certainly means address quality slipped, not that the domain is burnt. The reports are told to say
which it looks like.

**Drafts do not warm a domain. Only sent mail does.** If drafts pile up unsent, the ramp does not
advance — and at 40 a day, unsent drafts accumulate fast enough to be worth watching.

## Positioning — the facts, not the email copy

**The exact wording that goes in a Task 1 email is fixed inside
`task-1-startup-outreach/ROUTINE-INSTRUCTIONS.md` and that file is authoritative.** What follows
is the underlying claim, for reference and for the concept pages.

> Three years shipping production web and mobile systems, plus AI features on top of them.

Named proof point, when one is needed: **PureBody**, an AI fitness app live on Google Play.

**The Task 1 email never names a framework or a language.** No React, Next.js, Node, TypeScript
or AWS in the body. General capability attracts more founder interest than a stack list, and a
stack list in a cold email reads as a CV. The stack belongs on the CV and the portfolio, not in
the first two hundred words a stranger reads.

**Do not resurrect the "four years" version.** The 6 August run used an older paragraph that said
four years, which is both wrong and was not what he approved.

## Words that are banned in outreach copy

No em dashes anywhere. No exclamation marks. And none of these:

```
excited        thrilled       reach out      touch base      circle back
synergy        leverage       game-changer   revolutionary   cutting-edge
passionate     rockstar       ninja          10x             disrupt
I hope this email finds you well
I came across your company
```

**Name-masking note:** these are copy rules, not string filters. Never reject or rewrite a real
person's name because it collides with a banned word.

## The respect rules — both tasks, no exceptions

- **One company gets ONE first-touch email, ever.** Finding a better address later does not
  reopen it. A bounce is not retried at a different address unless Faisal asks.
- **One follow-up per person, ever.** It says plainly that it is the last one.
- **Never follow up on a thread that has a genuine human reply in it.** Ever.
- Anyone who asks not to be written to again is `OPTOUT`, permanently, immediately.
- **Never invent an email address or a phone number.** If it was not seen published on a page the
  run actually opened, it does not exist and the candidate is rejected.

## Never match on the string "Faisal"

The suppression list contains **Faisal Ilaiwi at `faisal@intunedhq.com`** — a different person,
a real prospect who was contacted on 4 August. A substring match on "Faisal" would silently
misfire against Faisal Hanif's own name.

Match on **exact email**, on **domain**, and on **full lowercased person name plus domain**.
Never on a fragment.

## Campaign calibration — what the numbers actually look like

65 sent 2 Aug · 29 on 4 Aug · 57 drafted later that day · 30 on 6 Aug · 26 on 7 Aug ·
11 on 14 Aug against a target of 20.

**~230 contacts have produced three human replies, one out-of-office and five bounces**, the
bounces dated 2 August (two), 4 August (two) and 6 August (one).

Every bounce came from a shared inbox. **No personal address published for a named person has
ever bounced.** That is the entire justification for the personal-address rule.

Expect roughly a **6 percent** hit rate from screened company to verified contactable founder.
A thin day is usually a correct outcome, not a tooling failure — which is why the routines make
the run distinguish *rejected* from *unreadable* and report the two separately.

## Preview page hosting (Task 3 only)

Hosting is manual. The run generates the HTML; Faisal uploads it to
`https://faisalhanif.work/p/<slug>`.

**The email carries the link only if the run fetched that exact URL and got HTTP 200.** No 200,
no link. This is a mechanism, not a warning — see README section 2 for why that distinction
cost four real businesses a broken link on 14 August.
