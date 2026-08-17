# Task 1 — setting up the Routine

This is the exact form. Every value has a reason next to it, because at least three of them have
been got wrong before and each mistake was expensive.

---

## Before you create anything

**1. Kill the old task on the other account.** A Routine named **"Daily job application prep
(9 AM)"** is still listed and still enabled on the account you were using before. It is the
scheduled job-search task that has been replaced by the interactive `Desktop/job-hunt/` flow.
Delete it, or at minimum toggle it off. Leaving it running spends budget on a pipeline nobody
reads any more.

**2. Push this folder to a private GitHub repository.** Private is not optional — `state/`
contains 257 real people with their email addresses.

**3. Do the two one-off state fixes** listed in the README's "Open items" section, before the
first scheduled run:

- Mark `mark@hugentic.ai` as `REPLIED` in `state/do-not-contact.md`. He replied at 13:04 UTC on
  14 August and the follow-up logic will otherwise reach him eventually.
- Reconcile the 26 rows dated 7 August that read `drafted` against Gmail Sent, plus the 5 rows
  reading `sent, FOLLOWED_1` whose follow-ups were never actually sent.

---

## The form

| Field | Value | Why |
|---|---|---|
| **Name** | `Task 1 — startup founder outreach (8 AM PKT)` | Name it so the two are never confused in the Routines list. Both draft from the same address; running the wrong one twice would blow the domain ceiling. |
| **Repository** | this repo, `main` | The routine reads `state/` and writes `state/` and `daily/` through git. |
| **Instructions** | paste `task-1-startup-outreach/ROUTINE-INSTRUCTIONS.md` **in full** | See the note below about pasting versus pointing. |
| **Schedule** | `0 3 * * *` | Cron is **UTC**. Faisal is UTC+5 with no daylight saving, so this is **08:00 Karachi**. Task 3 must stay two hours behind it. |
| **Model** | **Sonnet** | Not Opus. See below. |
| **Connectors** | **Gmail only** | See below. |
| **Auto-fix pull requests** | **OFF** | This routine's commits are data, not code. Nothing here needs a build fixed. |

### Paste the instructions in full — do not point at the file

It is tempting to write "read `task-1-startup-outreach/ROUTINE-INSTRUCTIONS.md` and follow it".
Don't. The ban block on the sending tools has to be in the run's context **before the toolbelt is
assembled**, not fetched at step one. That ordering is the entire fix for the 14 August incident.

When you edit the instructions later, edit the file in the repo **and** re-paste it into the form.
They will drift otherwise, and the copy in the form is the one that actually runs.

### Model: Sonnet, and this is not a cost preference

On 13 August the previous version of this pipeline was created from an **Opus** session. The old
scheduling API had no model parameter and a task permanently inherited the model of the session
that created it — so it ran on Opus every morning, and together with its siblings pushed a single
day's scheduled usage to roughly **9 percent** of the weekly limit against a 6 percent target.
Updating the prompt afterwards changed nothing.

The Routines form here **does** have a model field, so the inheritance trap is gone. The reason to
still pick Sonnet is the budget arithmetic: the call budgets in both routine files are sized so a
normal day lands at roughly **7 to 8 percent on Sonnet**. That headroom exists to buy volume —
more companies screened, more addresses verified — not a more expensive model. Opus would consume
it on its own and deliver fewer leads.

### Connectors: Gmail, and nothing else

Attach **Gmail**. Do not attach Google Drive, Calendar, Vibe Prospecting, or anything else.

Gmail is unavoidable, because `create_draft` is the whole point of the task. It is also
all-or-nothing: attaching it necessarily brings `send_message`, `reply` and `forward` along with
it. That risk cannot be engineered away from this side, which is exactly why the instructions
open with the ban block and why **Step 0a checks the Sent folder** before doing anything else.

**Vibe Prospecting charges real money** against a pipeline that is meant to cost nothing. If it is
attached to the account, make sure it is not selected here.

---

## After you save it

**Do not wait for 08:00 to find out whether it works.** Trigger one run manually and read the
report end to end. Check specifically:

1. **Step 0a reported the Sent-folder check** and found nothing. If it reports sent mail, stop
   everything and investigate before the next run.
2. **The blocked sets were built from `state/do-not-contact.md`** and the row count it reports
   matches the file.
3. **No freemail domain was blocked.** The report should say how many `(freemail)` rows it saw
   and confirm it blocked those addresses exactly rather than their domains.
4. **Every address in the output was quoted from a page the run opened**, with the URL recorded.
   Spot-check two of them by hand. This is the check worth doing every week for the first month.
5. **The git diff on `state/do-not-contact.md` is an append**, not a rewrite. Rows added, none
   removed. This is the thing git buys you that the old document store could not.

Then open Gmail and look at the drafts before sending any of them.

## What "a good morning" looks like

Around 20 drafts: five follow-ups and fifteen new companies. Sometimes fewer new ones, because
the hit rate from screened company to verified contactable founder is roughly 6 percent and some
mornings the pool is thin.

**A thin day where every address is real is a success. A full day with one invented address is a
failure.** The report is written to make that distinction visible — it separates *rejected*
(read the page, failed a filter) from *unreadable* (never got the page), and if unreadable
exceeds a quarter of pages attempted it opens with `TOOLING DEGRADED` in capitals. Read that line
first.
