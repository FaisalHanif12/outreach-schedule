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
new_companies_drafted:           /20
total_drafts:                    /25   (floor 15)

## Deliverability — READ THIS FIRST
bounces_last_24h:
bounce_rate_last_100_sent:       %     (>2% = open report in CAPITALS)
replies_last_24h:

## Lanes attempted — ALL EIGHT REQUIRED BEFORE A THIN DAY CAN BE DECLARED
| # | lane | screened | verified |
|---|---|---|---|
| 1 | YC pages and launch posts | | |
| 2 | HN Who is hiring, this month + last | | |
| 3 | Greenhouse / Lever / Ashby / Workable | | |
| 4 | Funding news, last 14 days | | |
| 5 | npm / PyPI maintainers | | |
| 6 | git commit author headers | | |
| 7 | Wellfound / WWR / RemoteOK | | |
| 8 | Near-miss reinstatements from the suppression list | | |

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

tool_calls:                      / 280 planned / 340 absolute
branch:                          run/task-N-YYYY-MM-DD
based_on:                        origin/main  /  run/... (unmerged, chained)
push_landed:                     yes / NO  (remote SHA:            )
pr_opened:                       yes / NO  (url:                     )

## Contact ledger — the two-touch invariant
rows at 1 touch (one follow-up still allowed):
rows at 2 touches (finished):
rows closed by REPLIED / BOUNCED / OPTOUT:
rows that would exceed 2 touches:            MUST BE 0
overrun_reason:
```

## Task 3 template

```markdown
# Task 3 — 2026-08-18

sent_check:                      clean / N MESSAGES FOUND
preflight:
existing_drafts_today:
ceiling_derived:                 min(15, 40 - N) =
trade_city_pairings:             US / UK / CA / AU / EU

## Deliverability — READ THIS FIRST
bounces_last_24h:
bounce_rate_last_50_sent:        %     (>2% = open report in CAPITALS)
replies_last_24h:

## Website leads
screened:
rejected:
dropped_on_spam_test:            (and which numbered check failed)
UNREADABLE (counted separately):
drafts_created:                  /15   (floor 10)
  with a verified link:
  shipped without a link:        slugs needing upload:

## Regional split — TWO PAIRINGS PER REGION MINIMUM BEFORE STOPPING BELOW 15
| region | pairing 1 | pairing 2 | leads |
|---|---|---|---|
| US | | | |
| UK | | | |
| CA | | | |
| AU | | | |
| EU | | | |
(a region at zero three mornings running means its sourcing needs changing,
 not that the region gets quietly dropped)

## Call leads
profiles_opened:
website_field_genuinely_absent:
delivered:                       /3
  grade 1:
  grade 2 (localsearch microsite):

preview_pages_generated:
tracker_rows_before / after:
tool_calls:                      / 280 planned / 340 absolute
call_lead_calls_spent:           / 15 hard cap
branch:                          run/task-N-YYYY-MM-DD
based_on:                        origin/main  /  run/... (unmerged, chained)
push_landed:                     yes / NO  (remote SHA:            )
pr_opened:                       yes / NO  (url:                     )

## Contact ledger — the two-touch invariant
rows at 1 touch (one follow-up still allowed):
rows at 2 touches (finished):
rows closed by REPLIED / BOUNCED / OPTOUT:
rows that would exceed 2 touches:            MUST BE 0
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
