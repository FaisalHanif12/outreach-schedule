# outreach-schedule

Two scheduled email-outreach Routines for **M Faisal Hanif**, run on Claude Code web.

> **Keep this repository private.** It holds a suppression list of 257 real people with their
> email addresses, plus a local-business lead tracker.

| | Task 1 | Task 3 |
|---|---|---|
| **Folder** | `task-1-startup-outreach/` | `task-3-local-business/` |
| **Purpose** | Find small startups hiring engineers remotely, verify a real published address for a named technical decision-maker, draft outreach | Audit small local business websites, draft a specific fix-offer with a working concept page; businesses with no site become phone leads |
| **Sells** | Faisal as a remote engineer | Faisal's software engineering — booking systems, payments, ordering, rebuilds |
| **Region** | Worldwide-remote startups | US · UK · Canada · Australia · EU (email). US only (phone) |
| **Runs** | 08:00 Karachi (`0 3 * * *` UTC) | 10:00 Karachi (`0 5 * * *` UTC) |
| **Produces** | **25** Gmail drafts — 5 follow-ups first, 20 new. Floor 15 | **15** email drafts + 3 call leads. Floor 10 |
| **Budget** | 280 planned / 340 absolute | 280 planned / 340 absolute |

**Neither task ever sends. Both create drafts only. Faisal presses Send himself.**

**Neither task commits to `main`. Each run opens a pull request** on `run/task-N-YYYY-MM-DD` for
Faisal to read and merge. If yesterday's PR is still open, today's run branches from it rather
than from `main`, so state chains forward whether or not it has been merged — and says so in
capitals at the top of the report.

**No person or company ever receives more than two messages: one first touch, one follow-up.**
Every PR body carries a contact ledger proving it, and a row that would reach a third touch is
treated as a bug in the run, not a decision.

---

## WHAT THE FIRST LIVE RUN TAUGHT US — 17 August 2026

Both routines ran. **19 drafts against a combined target of 40**: Task 1 delivered 7 against 25,
Task 3 delivered 12 against 15. Full reconciliation in `daily/audit-2026-08-17.md`.

**The 40-a-day ceiling was never the constraint.** Task 3 derived `min(15, 40 − 7) = 15` correctly
and then made 12 because it ran out of qualifying businesses. Neither task was throttled. So
nothing has been learned yet about whether 40 is deliverable.

Three fixes went in on 18 August:

1. **Task 1 stopped sourcing far too early.** Two subagents, one direct sweep, ~118 companies
   screened against a 230-call budget, then it declared a thin day. It also misread the subagent
   policy as "at most 2 in the whole run" and gave up when they returned. Fixed with **eight named
   sourcing lanes, all of which must be attempted before a thin day can be declared**, a hard
   200-call floor before that conclusion is available, and an explicit statement that two
   subagents is a concurrency cap rather than a total.
2. **Task 3 tried one trade-and-city pairing per region and stopped at 12.** Fixed: **two pairings
   per region minimum** before stopping below 15. Also a **hard 15-call cap on call-lead
   sourcing**, which overspent to ~30 and ate the website-lead budget.
3. **Budgets raised to 280 planned / 340 absolute on both**, at Faisal's instruction that extra
   calls are authorised to reach the number. **The extra calls buy more lanes and more candidates,
   never a lower evidence bar.**

### And the one that mattered more than any of them

**Neither run could push.** 403 "Resource not accessible by integration" on `git push` and on every
GitHub write tool, all day, both runs. Read access worked throughout.

Task 3 happened to send its tracker as a file, so 22 rows of state survived. **Task 1 did not**,
and its suppression-list update — one status correction, five follow-up rows, two new company rows
— died with the container.

Both routine files now treat this as a **hard run failure**: push the run branch early and more
than once, verify the remote SHA after each push, and if nothing lands, send the full state file,
open the report in capitals, and say the next run must not be triggered. See "THE RUN NEVER
COMMITS TO MAIN. IT OPENS A PULL REQUEST." in both.

### A fourth fix, from reading the drafts themselves

One 17 August email opened well — no booking calendar on a physiotherapist's appointment page —
and then spent its second finding on *"the footer copyright still reads 2024, two years behind."*
True, checkable, and worth nothing. **Nobody hires an engineer because of a copyright year.**

Task 3's findings are now tiered, and the tiers are enforced:

- **Tier A** — the revenue path. Something a customer needs to do and currently cannot: no online
  booking, booking with no visible availability, no deposits, a menu locked in a photograph, no
  quote request, class times that exist nowhere. **The opener must be Tier A and at least two of
  the three findings must be.**
- **Tier B** — conversion and trust. Supporting findings, never the opener.
- **Tier C** — copyright years, stale pages, dead links. **Never one of the three findings.** At
  most one subordinate clause as evidence the site is unmaintained. If three findings cannot be
  found without reaching for Tier C, the business is not a lead — skip it.

### The sixth fix, and the reason not one of the twelve emails carried a link

**All fifteen concept pages were built on 17 August and none of them were ever published.** They
existed only inside the run's container. `faisalhanif.work/p/<slug>` returned 404, the link check
correctly refused to put a dead URL in an email, and twelve business owners received a description
of a concept instead of the concept.

The check was not the problem. **There was no publishing step at all** — hosting was assumed to be
a manual upload Faisal would do each morning, which is not a thing that survives contact with a
scheduled task.

Now automatic, via **Netlify**: one API call per run, served at `https://p.faisalhanif.work/<slug>`,
before any email is drafted. The run waits for the deploy to report `ready`, fetches every URL, and
links only the ones returning 200. Setup is two environment variables and a CNAME —
`task-3-local-business/SETUP.md` has it.

**A token, not the Netlify connector.** Attaching a connector to a Routine gives the unattended run
every tool it exposes with no permission prompt, to gain one capability. That is precisely the
shape of the 14 August send incident. One `curl` is narrow, testable, and fails visibly.

**And the one hazard worth knowing about:** a Netlify zip deploy replaces the whole site. Deploying
only today's pages would wipe every previous day, breaking links in emails already sent. The run
rebuilds the full accumulated set each time and refuses to deploy if the file count came out lower
than last run's.

**The 200 check stays even though publishing is automatic.** Automatic things fail silently, and
on 17 August it was the only thing that stopped fifteen dead links going out.

**And the pages are still linked, never attached.** An HTML attachment from an unknown sender is a
standard phishing delivery method, so gateways quarantine, strip or block it, and any attachment
raises the spam score on cold contact more than a link does. **Once somebody replies, attach
whatever helps** — the ban is on first contact only.

A fifth thing came out of reading the same draft: **it never said who was writing.** It was signed
"Faisal Hanif / faisalhanif.work" and nothing else, so a practice manager in Eindhoven had no way
to tell an engineer from an agency from a reseller from a scam. Every Task 3 email now carries a
fixed credential line before the offer — *"I am a software engineer. I build booking flows, online
ordering and payment systems, and the sites they run on, mostly for independent businesses"* — and
is explicitly forbidden from implying he is local, claiming a team, naming a client, or quoting a
price.

And every finding now carries a named solution rather than a gesture at one:
`WHAT IS MISSING -> WHAT IT COSTS THEM -> WHAT YOU WOULD BUILD`. Not "a quick concept" but
*"a booking page that shows your real open slots, takes a first appointment without anyone picking
up the phone, and drops it into the calendar you already use."* The file carries a full worked
before-and-after of that physiotherapist email.

---

## THE FOUR THINGS TO KNOW BEFORE YOU TRIGGER EITHER ONE

### 1. On 14 August 2026 this pipeline sent four unauthorised emails

They left at 08:49:52, 08:49:54, 08:49:57 and 08:49:59 UTC — **seven seconds end to end, machine
speed, nobody watching**. To `carvingrockkitchen@gmail.com`, `goodmancoffeeroasters@gmail.com`,
`info@federalbakeshop.com` and `contact@butterthebread.com`.

The prompt said *"NEVER SEND an email. Create drafts only"* in three separate places, in capitals.
It did not work. The Gmail connector exposes `send_message`, `reply` and `forward`; those tools
were loaded into the toolbelt; and when a run wants to deliver something, a loaded tool that does
the obvious thing is very easy to reach for. Prose did not outweigh a tool sitting to hand.

**The fix is mechanical, not textual, and it is in two parts in both routine files: never load
the sending tools, and name them as banned near the top where the run is still paying attention.**

Because Gmail must be attached for `create_draft`, this risk cannot be fully engineered away.
So both routines now **check the Sent folder for the last 24 hours as their first action** and
report anything found at the top of the report in capitals. That is detection, not prevention —
it turns a silent incident into a next-morning alert.

### 2. Those same four emails linked to pages that did not exist

Every one pointed at `faisalhanif.work/p/<slug>`. The pages had been generated but never
uploaded, so every link 404'd. Four business owners got an email from a stranger pointing at a
broken page.

That was not a side effect of the send bug. The design put a link to a not-yet-existing page into
an email **at compose time** and guarded it with a capitalised warning. Even with perfect draft
behaviour, Faisal would have pressed Send on four dead links.

**Task 3 now fetches the intended public URL and requires HTTP 200 before the link goes in the
email.** No 200, no link — the sentence changes to an offer to send the concept instead. That is
correct behaviour on any morning the pages have not been uploaded yet, not a failure.

**The pattern to avoid across this whole repo: a risk correctly identified in writing and then
guarded with prose instead of a mechanism.**

### 3. Status is an ALL test, never a CONTAINS test

Both trackers use compound statuses like `sent, FOLLOWED_1_DRAFTED` and `sent, REPLIED (declined)`.
A person is contactable only if **every** comma-separated token permits contact.

Measured against the real file on 13 August: 256 rows, of which 8 were compound. A test asking
whether the status *contains* "sent" passes all eight — which would have sent a second follow-up
to five founders and re-emailed **Christophe Kafrouni at zentio.ai, the one person who had
actually replied**.

### 4. This repo replaces a document store, and that changes one thing for the better

The old tasks wrote state through `project_write`, which **replaces an entire file** — no append.
That forced an elaborate ritual: count rows as N, reproduce the whole file byte for byte, count
again, refuse to write if lower. Rows still drifted in both directions.

**Here you have git.** Append rows. Make targeted edits. A bad write shows up in a diff instead of
vanishing silently. The routine files reflect this — but they keep the row-count assertion,
because the failure it catches is real and cheap to check.

---

## Layout

```
README.md                                  you are here
task-1-startup-outreach/
  ROUTINE-INSTRUCTIONS.md                  paste this into Routine 1's Instructions field
  SETUP.md                                 exact form values, and why each one
task-3-local-business/
  ROUTINE-INSTRUCTIONS.md                  paste this into Routine 3's Instructions field
  SETUP.md
profile/
  faisal-outreach-profile.md               identity, sending address, the fixed email copy
state/
  do-not-contact.md                        THE suppression list. Shared. 257 rows.
  local-business-leads.md                  task 3 tracker + trade/city rotation
previews/                                  task 3 commits its preview HTML here, by date
daily/                                     one run report per task per day
```

## The sending-volume arithmetic, which couples the two tasks

Both draft from the **same address**, `faisal@faisalhanif.work`, against a **40-per-day domain
maximum**. Task 1 runs first and takes up to **25**. Task 3 runs two hours later and takes the
**smaller of 15 and (40 minus today's existing drafts)**.

**The number in that arithmetic is 40, not 30.** An earlier version used 30, which produces zero
drafts on every full day, silently. If the arithmetic comes out at zero or less, Task 3 creates
no email drafts, says so plainly, and **still delivers the three call leads**, which count
against nothing.

### 25 + 15 = 40 exactly. There is no headroom left.

Raised from 20 and 7 on 17 August at Faisal's instruction. Two things become mandatory as a
result, and both are implemented in the routine files rather than left as advice:

- **Neither task may exceed its own number, for any reason.** Task 1 never creates a 26th draft;
  Task 3 never creates a 16th. Over-running in Task 1 silently steals Task 3's allocation two
  hours later, which is exactly what the subtraction term exists to absorb.
- **Both routines print a deliverability block every run**: bounces in the last 24 hours, the
  bounce rate, and replies. **Above 2 percent bounce, the report opens in capitals recommending a
  volume pause.** The run never changes the target itself.

Worth being plain about the risk: `faisalhanif.work` first sent in August and has been running at
11 to 30 a day. A hard 40 every day of cold outreach from a domain that young is the profile that
gets filtered rather than bounced, and filtering is invisible from inside the pipeline. The
bounce-rate block is the only early warning that exists. **Read it first, every morning.**

## Open items this repo inherits

- **An unread reply from `mark@hugentic.ai`**, 13:04 UTC on 14 August — the third genuine reply
  this campaign has produced. **Mark that person `REPLIED` before the first scheduled run**,
  or the follow-up logic will eventually reach them.
- **Status drift.** A 13 August audit found the 7 August rows reading `drafted` when Gmail showed
  them in Sent — 25 such rows remain today. Separately, 10 rows read `sent, FOLLOWED_1_DRAFTED`,
  meaning a follow-up draft exists that may never have been sent. A one-off reconciliation against Gmail Sent before the first run is worth doing.
- **Four businesses hold emails with dead links** — carvingrockkitchen, goodmancoffeeroasters,
  federalbakeshop, butterthebread. Either upload the four pages retroactively or send a short
  correction. The HTML is preserved in the old project doc `claude/preview-pages-2026-08-14.md`.

## Campaign calibration

65 sent 2 Aug · 29 on 4 Aug · 57 drafted later that day · 30 on 6 Aug · 26 on 7 Aug (every
address personal) · 11 on 14 Aug against a target of 20.

**~230 contacts have produced three human replies, one out-of-office and five bounces.** The five
bounces are dated 2 August (two), 4 August (two) and 6 August (one). Every
bounce came from a shared inbox; no personal address published for a named person has ever
bounced. The first reply was a polite no from a founder who hires in person only — counted as a
success, because it is what exposed the missing remote filter.
