# daily/

One file per task per day, committed by the run itself.

```
daily/task-1-2026-08-18.md
daily/task-3-2026-08-18.md
```

The point is that in a month you can see whether the method is working without re-reading a
transcript. Keep them short and factual.

---

## Task 1 template

```markdown
# Task 1 — 2026-08-18

sent_check:                      clean / N MESSAGES FOUND
preflight:                       websearch OK, webfetch OK, exa 402, apify absent
suppression_rows_read:
freemail_rows_seen:

follow_ups_drafted:              /5
new_companies_drafted:           /15
total_drafts:                    /20

companies_screened:
rejected_shared_inbox_only:
rejected_no_headcount_stated:
rejected_remote_us_only:
rejected_other:
UNREADABLE (counted separately):

## Sources that produced a verified contact
| source | screened | verified |
|---|---|---|

## Near misses worth keeping
(company, what it failed on, and what would reinstate it)

tool_calls:                      / 180 planned / 225 absolute
overrun_reason:
```

## Task 3 template

```markdown
# Task 3 — 2026-08-18

sent_check:                      clean / N MESSAGES FOUND
preflight:
existing_drafts_today:
ceiling_derived:                 min(7, 40 - N) =
trade_city_pairing:

## Website leads
screened:
rejected:
UNREADABLE (counted separately):
drafts_created:                  /7
  with a verified link:
  shipped without a link:        slugs needing upload:

## Call leads
profiles_opened:
website_field_genuinely_absent:
delivered:                       /3
  grade 1:
  grade 2 (localsearch microsite):

preview_pages_generated:
tracker_rows_before / after:
tool_calls:                      / 110 planned / 140 absolute
overrun_reason:
```

---

## Why the source and rejection tables matter

The job-search task this pipeline sits beside once spent **605 postings across the eleven biggest
job boards and got zero usable roles out of them.** Nobody noticed for two weeks, because
per-source yield was never recorded — every day just looked like a thin day.

Record it every run, and prune. **Three barren runs in a row and a source gets demoted**, with the
date and the count written down.

The same applies to the rejection reasons. If `rejected_shared_inbox_only` is the top line every
morning for a week, the sourcing lane is wrong, not the filter. That is a decision Faisal can only
make if the number is in front of him.
