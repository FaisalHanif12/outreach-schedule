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
| **Model** | **Sonnet** | Same reasoning as Task 1. The 280-call budget is sized for Sonnet. |
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

### The GitHub App needs WRITE access — check this before anything else

On 17 August both routines got `403 Resource not accessible by integration` on every write path
while reading fine all day. Task 3 was lucky: it sent its tracker as a file, so 22 rows survived.
Task 1 was not, and lost its suppression-list update entirely.

`github.com/settings/installations` → **Claude** → **Configure**:

- **Repository access** includes `outreach-schedule`
- **Permissions → Contents** reads **Read and write**, not Read-only. Approve any pending
  permission request shown at the top of that page.

**A run that cannot push has failed**, and both routine files now say so in capitals rather than
reporting success with a caveat.

Each run opens a PR on `run/task-3-YYYY-MM-DD` rather than committing to `main`. Read the body and
merge it daily. If you do not, the next run branches from the unmerged branch instead of `main` so
state still chains correctly, but it will tell you in capitals how many are outstanding.

## ONE-TIME: set up Netlify hosting, or every email ships without a link

**This is why the 17 August drafts had no link.** All fifteen concept pages were built correctly
and none were ever published, so the public URL returned 404 and the link check refused to put a
dead URL in an email. The check did its job. The publishing step did not exist.

Ten minutes, once.

### Why Netlify and not the GitHub Pages plan

Netlify deploys in five to twenty seconds against thirty to ninety for Pages, needs no second
repository, and is a single API call. Pages would also have meant either a second repo or exposing
`state/do-not-contact.md` on a public URL, since Pages publishes everything on the branch it serves.

### Why an API token and not the Netlify connector

There **is** a Netlify connector in the registry, and attaching it to the Routine would work. Don't.

Look at the warning on the Routine form: *"Claude can use all tools from these connectors —
including writes — without asking for permission during runs."* Attaching Netlify hands an
unattended run the ability to delete sites, change DNS and rewrite environment variables, to gain
one capability: uploading a zip.

**That is exactly the shape of the 14 August incident** — Gmail had to be attached for
`create_draft`, `send_message` came with it, and four unauthorised emails went out. Gmail is
unavoidable. Netlify is not: one `curl` with a token gets the same result, is testable, and fails
visibly in the report instead of opaquely inside a tool call.

### 1. Create the site

Netlify → **Add new site** → **Deploy manually** → drag any folder with an `index.html` in it. The
content does not matter; you are creating the site so it has an ID.

Rename it to something presentable while you are there.

### 2. Get the two values

- **Site ID:** Site configuration → General → Site details → **API ID**
- **Token:** User settings → Applications → **Personal access tokens** → New access token

### 3. Point your subdomain at it

- Netlify → Domain management → Add a domain → `p.faisalhanif.work`
- In your DNS: CNAME `p` → `<your-site>.netlify.app`

Links then read `https://p.faisalhanif.work/oakleaf-barbers.html`. Worth doing before the first
real run — a `random-name-84213.netlify.app` link in a cold email from a stranger undoes some of
the credibility the concept page is there to build.

### 4. Give both values to the Routine

Task 3 Routine → cloud environment settings → add:

```
NETLIFY_TOKEN    = <personal access token>
NETLIFY_SITE_ID  = <API ID>
```

### The one thing that can go badly wrong

**A Netlify zip deploy replaces the whole site.** Deploy only today's fifteen pages and every page
from every previous day vanishes — including URLs sitting in emails already in people's inboxes.

The routine handles this: it rebuilds the full site from `previews/**` across all dates plus
today's, counts the files, and **refuses to deploy if the count is lower than last time.** Check
that count in the report for the first week. If it ever drops, something is wrong with the branch
it based on.

### What the run does, unattended

Builds the pages → assembles the accumulated site → deploys one zip → polls until `ready` →
fetches every URL → **links only the ones returning 200.**

If any of that is missing or fails, the run says which step and every email ships link-free,
offering to send the concept instead. Safe day. **Do not "fix" a link-free morning by relaxing the
200 check.**

## Before the first run

**Verify the tracker is in the repo and readable, and that it is the 22-row version.** The
17 August run appended 15 rows (7 → 22) but could not push them; it sent the updated file to Faisal
directly. **That file must be back in the repo before the next run**, or Task 3 will re-contact the
twelve businesses it drafted yesterday. If the tracker does not read at all, the routine stops, by
design.

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
7. **The push landed.** The report must name the verified remote SHA. On 17 August nothing pushed
   all day and both runs still reported success — that is now a hard failure.
8. **Call-lead sourcing stayed inside its 15-call cap.** It burned ~30 on 17 August and that
   overspend came out of the website-lead budget.
9. **Every region shows two trade-and-city pairings** if the run finished below 15.
10. **Every email opens on a Tier A finding** — a missing or broken revenue path, not a copyright
    year. At most one Tier C reference in the whole email, in a subordinate clause.
11. **Every email names the specific thing that would be built.** "A booking page that shows your
    real open slots and drops the appointment into the calendar you already use", not "a quick
    concept" or "improvements to your booking".
12. **Every email carries the credential line** — "I am a software engineer. I build booking flows,
    online ordering and payment systems, and the sites they run on, mostly for independent
    businesses." Without it the recipient cannot tell an engineer from an agency from a scam, and
    the default assumption for an unsolicited website email is not a kind one.
13. **No email implies he is local.** No "here in <city>", no "a local developer", no "we". Not
    stating a location is fine; implying the wrong one is not.
14. **Every email that should carry a link does.** The report splits leads into "carries a verified
    link" and "shipped without one". Once Netlify is set up, the second group should be empty on a
    normal morning — if it is not, publishing broke and the report will name which step.
    **Also check the deployed page count**: it must never be lower than the previous run's, or
    older pages have been wiped and links in already-sent emails are now dead.
15. **No draft has an attachment.** Not one. Links only on first contact.

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
