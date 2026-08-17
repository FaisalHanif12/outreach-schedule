# Task 3 — setting up the Routine

Set this one up **after** Task 1, and read Task 1's SETUP.md first. Most of the reasoning is
shared and is not repeated here.

---

## The form

| Field | Value | Why |
|---|---|---|
| **Name** | `Task 3 — local business leads (10 AM PKT)` | Distinct from Task 1 at a glance. They draft from the same address; confusing them would blow the domain ceiling. |
| **Repository** | this repo, `main` | Reads and writes `state/local-business-leads.md`, commits previews to `previews/` and the packet to `daily/`. |
| **Instructions** | paste `task-3-local-business/ROUTINE-INSTRUCTIONS.md` **in full** | The ban block must be in context before the toolbelt is assembled. Do not replace it with a pointer. |
| **Schedule** | `0 5 * * *` | UTC. Faisal is UTC+5 with no daylight saving, so **10:00 Karachi**. |
| **Model** | **Sonnet** | Same reasoning as Task 1. The 230-call budget is sized for Sonnet. |
| **Connectors** | **Gmail only** | Not Vibe Prospecting, which charges real money. Not Drive, not Calendar. |
| **Auto-fix pull requests** | **OFF** | |

## The two-hour gap is load-bearing, not cosmetic

Task 3 derives its email ceiling as `min(15, 40 - drafts already created today)`. That arithmetic
only works if **Task 1 has already finished and its drafts exist** when Task 3 counts them.

`0 3 * * *` and `0 5 * * *`. Two hours. **If you ever move Task 1, move Task 3 with it.**

If they overlap, Task 3 counts a Drafts folder that Task 1 has not filled yet, so the subtraction
returns its full fifteen no matter what Task 1 did. On a clean day that still lands on exactly 40.
On any day Task 1 over-ran, or ran twice, or a manual trigger doubled it, nothing catches it.

That mattered less at 20 + 7 = 27 against 40, where thirteen spare absorbed the mistake. **At
25 + 15 = 40 the subtraction is the only safety net there is**, so the gap is now doing real work
rather than being tidy.

## Before the first run

**Verify the tracker is in the repo and readable.** `state/local-business-leads.md` should have
seven rows under `## The list` — four Category A (all `drafted`, greater Chattanooga TN,
14 August) and three Category B (all `queued`, Knoxville TN). If it does not read, the routine
stops, by design.

**Decide what to do about the four dead links.** carvingrockkitchen, goodmancoffeeroasters,
federalbakeshop and butterthebread are holding emails pointing at pages that 404. The HTML for all
four is in the old project doc `claude/preview-pages-2026-08-14.md`. Either upload the four pages
to `faisalhanif.work/p/` so the links resolve, or send a short correction. This does not block the
routine — the link check stops it recurring either way — but those four people currently have a
broken link from a stranger in their inbox.

**Note that on day one every email will ship without a preview link.** The pages are generated the
same morning they are drafted, so nothing is live at that URL yet unless you upload before 10:00.
The report will say so. **That is the mechanism working, not a bug.** Do not "fix" it by relaxing
the 200 check.

---

## After you save it

Trigger one run manually and read the report before letting it run on schedule. Check:

1. **Step 0a reported the Sent-folder check** and found nothing unexpected.
2. **The ceiling it derived** is a number, and the number makes sense against what Task 1 did that
   morning.
3. **`bbb.org` does not appear anywhere in the run.** It is dead from this environment and any
   call spent on it is wasted.
4. **Every Category B lead carries a grade**, 1 or 2, and the grade-2 ones explain the
   `*.localsearch.com` reasoning.
5. **Open three of the fifteen website leads yourself and check the three findings.** This is the
   single most valuable check for the first two weeks. Every finding is a claim made to a stranger
   about their own business, and one false claim loses the prospect permanently.
6. **The git diff on `state/local-business-leads.md` is an append.** Rows added, none removed.

Then open Gmail and read the drafts before sending any.

## What "a good morning" looks like

**Target 15 email drafts and 3 call leads. Floor 10.** The fifteen spread across the five regions
— US, UK, Canada, Australia and the EU — roughly three each.

Each email carries three true findings **plus one line on what they cost the business**, and each
lead gets a concept page that demonstrates the fix rather than describing it. Check the report's
regional split: if one region produces nothing three mornings running, the sourcing approach for
it needs changing rather than the region being quietly dropped.

**Read the deliverability block first** — bounces, bounce rate, replies. At 25 + 15 the domain is
at its full 40-a-day ceiling with no slack, so that number is the only early warning that exists.

**A thin day where every finding is true is a success.** The report separates *rejected* (read the
page, failed a filter) from *unreadable* (never got the page), and opens with `TOOLING DEGRADED`
in capitals if unreadable exceeds a quarter of pages attempted. Read that line first — it is the
difference between "the pool was thin this morning" and "the run was broken and produced garbage".

## What this task will never do, no matter how it is asked

- **Email a business that has no website.** No free source publishes those addresses; every
  directory holding one puts it behind a relay form. Tested across thirty calls on 13 August.
  Faisal has asked for this more than once. It remains three phone calls until a source turns up
  that publishes addresses openly.
- **Submit a directory relay form.**
- **Plan or send automated SMS.** US TCPA rules on automated texting are considerably stricter
  than the rules on email.
- **Make a claim about HTTPS or certificates.** Not determinable from this environment.
- **Send anything.** Drafts only. Faisal presses Send.
