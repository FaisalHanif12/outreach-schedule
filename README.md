# outreach-schedule

Two scheduled email-outreach Routines for **M Faisal Hanif**, run on Claude Code web.

> **Keep this repository private.** It holds a suppression list of 257 real people with their
> email addresses, plus a local-business lead tracker.

| | Task 1 | Task 3 |
|---|---|---|
| **Folder** | `task-1-startup-outreach/` | `task-3-local-business/` |
| **Purpose** | Find small startups hiring engineers remotely, verify a real published address for a named technical decision-maker, draft outreach | Audit small local business websites, draft a specific fix-offer; businesses with no site become phone leads |
| **Sells** | Faisal as a remote engineer | Faisal's web design and development services |
| **Runs** | 08:00 Karachi (`0 3 * * *` UTC) | 10:00 Karachi (`0 5 * * *` UTC) |
| **Produces** | 20 Gmail drafts — 5 follow-ups first, 15 new | 7 email drafts + 3 call leads |
| **Budget** | 180 planned / 225 absolute | 110 planned / 140 absolute |

**Neither task ever sends. Both create drafts only. Faisal presses Send himself.**

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

Both trackers use compound statuses like `sent, FOLLOWED_1` and `sent, REPLIED (declined)`.
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
maximum**. Task 1 runs first and takes up to 20. Task 3 runs two hours later and takes the
**smaller of 7 and (40 minus today's existing drafts)**.

**The number in that arithmetic is 40, not 30.** An earlier version used 30, which produces zero
drafts on every full day, silently. If the arithmetic comes out at zero or less, Task 3 creates
no email drafts, says so plainly, and **still delivers the three call leads**, which count
against nothing.

## Open items this repo inherits

- **An unread reply from `mark@hugentic.ai`**, 13:04 UTC on 14 August — only the second genuine
  reply this campaign has produced. **Mark that person `REPLIED` before the first scheduled run**,
  or the follow-up logic will eventually reach them.
- **Status drift.** A 13 August audit found 26 rows dated 7 August reading `drafted` when Gmail
  showed all 26 in Sent, and 5 rows reading `sent, FOLLOWED_1` when those follow-ups were still
  unsent drafts. A one-off reconciliation against Gmail Sent before the first run is worth doing.
- **Four businesses hold emails with dead links** — carvingrockkitchen, goodmancoffeeroasters,
  federalbakeshop, butterthebread. Either upload the four pages retroactively or send a short
  correction. The HTML is preserved in the old project doc `claude/preview-pages-2026-08-14.md`.

## Campaign calibration

65 sent 2 Aug (4 bounces) · 29 on 4 Aug (1 bounce) · 57 drafted later that day · 30 on 6 Aug ·
26 on 7 Aug (every address personal) · 11 on 14 Aug against a target of 20.

**~230 contacts have produced two human replies, one out-of-office and five bounces.** Every
bounce came from a shared inbox; no personal address published for a named person has ever
bounced. The first reply was a polite no from a founder who hires in person only — counted as a
success, because it is what exposed the missing remote filter.
