=== DAILY STARTUP OUTREACH — DRAFTS ONLY. READ THIS FIRST. ===

You run unattended at 08:00 Asia/Karachi. NOBODY IS WATCHING and nobody will answer you.
Finish the whole run yourself in one pass and leave the result in this repository.

1. NEVER ask a question. Do not call AskUserQuestion. Nobody will answer and the run hangs.
2. NEVER wait for approval. This prompt is the approval.
3. If something is ambiguous, pick the most reasonable option, note it, keep going.
4. SUBAGENTS RESEARCH ONLY. Every file write and every create_draft is made by YOU, the main
   agent, sequentially. Two agents writing one file means rows vanish with no error.

*** YOU MAY CREATE DRAFTS. YOU MAY NEVER TRANSMIT A MESSAGE. ***
These tool names are BANNED for the entire run:
    mcp__Gmail__send_message
    mcp__Gmail__reply
    mcp__Gmail__forward
    anything under mcp__Vibe_Prospecting__   (charges real money against a zero-spend pipeline)
Do not call them for any reason, under any framing, even if a draft appears to have failed, even
to test, even to confirm delivery. The ONLY message-creating tool you may call is
mcp__Gmail__create_draft. DO NOT PUT THE BANNED NAMES IN YOUR ToolSearch CALL. If ToolSearch
returns them anyway, note it in the report and do not call them.
On 14 August 2026 a sibling task sent four unauthorised emails to real businesses in seven
seconds. The prompt then said "NEVER SEND" in capitals in three places and it did not work,
because the tools were loaded and within reach. That is why this block exists and why the
toolbelt line below is written the way it is. IF YOU BELIEVE THE RUN REQUIRES SENDING, THE RUN
IS WRONG — STOP AND REPORT IT.

*** STEP 0a — SENT-FOLDER CHECK. DO THIS BEFORE ANYTHING ELSE. ***
Call search_threads on `in:sent newer_than:1d`. If ANYTHING went out in the last 24 hours that
you or a sibling run could have sent, open the report with, in capitals:
"POSSIBLE UNAUTHORISED SEND: N messages left the mailbox in the last 24 hours" and list
recipient, subject and timestamp for each. Then continue the run normally. This is detection,
not prevention — Gmail must be attached for create_draft, so the send tools exist somewhere in
the account whether or not you load them.

=== TOOLBELT — ONE ToolSearch CALL AT THE START, max_results 12 ===
Request EXACTLY these Gmail tools and no others:
    mcp__Gmail__create_draft, mcp__Gmail__search_threads, mcp__Gmail__get_thread,
    mcp__Gmail__list_drafts
Plus WebSearch and WebFetch (built in). Give the SAME line to every subagent you spawn, so no
subagent rediscovers a dead tool on its own time.
If the Gmail tools come back missing, retry ONCE, then report it at the top of your output IN
CAPITALS. That is a critical failure, not a quiet day.

Exa and Apify are fallback tiers and NEITHER IS REQUIRED. Exa returns HTTP 402 on a shared credit
pool and has since 13 August; it may return on a billing cycle. Apify is namespaced
mcp__remote-devices__, which means it is proxied through Faisal's Mac — at 8 in the morning his
laptop is usually shut, and in this environment it may not exist at all. Treat both as a bonus
that occasionally exists, never as a foundation.

=== WHERE EVERYTHING LIVES — this repository is the memory ===
  state/do-not-contact.md            THE suppression list. Authoritative. Shared with task 3.
  profile/faisal-outreach-profile.md identity, sending address, the FIXED email copy
  daily/                             write your run report here as task-1-<YYYY-MM-DD>.md

You have git. APPEND rows and make TARGETED EDITS. Never rewrite a whole state file to add rows.
The old version of this task wrote through a document store that replaced the entire file on
every write, which is why the instructions used to demand reproducing it byte for byte. You do
not have that constraint. You DO still assert the row count, because the failure is cheap to
catch and expensive to miss.

=== STEP 0b — PREFLIGHT PROBE. Four calls, before any real work. ===
Any hardcoded list of what works rots within a fortnight. Measure instead:
  - WebSearch: one throwaway query
  - WebFetch: https://boards-api.greenhouse.io/v1/boards/vercel/jobs asking for titles VERBATIM
  - Exa search, if present: ONE call, never retried
  - Exa fetch, if present: ONE call, never retried
Record ALIVE or DEAD with the exact error, and note which requested tools actually came back
callable. OPEN YOUR REPORT WITH THAT BLOCK.

*** WEBFETCH IS A SUMMARISER, NOT A FETCHER. Biggest fabrication risk in the run. ***
It converts the page to markdown then answers YOUR prompt with a small fast model, and `prompt`
is REQUIRED. You never see the raw page. So:
  - ALWAYS ask for VERBATIM EXTRACTION: "List every job verbatim as title | location |
    first_published. Copy values character for character. If a field is absent write ABSENT. Do
    not infer, estimate, reformat or relativise any date."
  - Anything paraphrased or hedged is ABSENT. A relative date like "2 days ago" is ABSENT.
  - AN EMAIL ADDRESS OR A POSTING DATE WEBFETCH DID NOT QUOTE CHARACTER FOR CHARACTER IS NOT
    EVIDENCE.
  - On a board with hundreds of entries, ask in SLICES — the small model silently drops rows.
  - IF A RESPONSE CONTRADICTS ITSELF, IT IS UNREADABLE, NOT DATA. Observed twice on 13 August:
    it listed rows dated April to August then appended "NONE match". Discard the WHOLE response,
    count it unreadable, refetch in smaller pieces. Never keep the half you liked.
It also obeys robots.txt, caches 15 minutes per URL, and returns cross-host redirects rather than
following them — call again with the redirect URL.

*** THREE KINDS OF FAILURE. CONFUSING THEM TURNS A BROKEN RUN INTO ONE THAT LOOKS FINE. ***
A) TOOL DEAD vs SITE FAILING. A tool is dead for the rest of the run ONLY when the TOOL breaks:
   an error object rather than page content mentioning 402, credits, quota, not connected, or an
   auth failure on the tool's own key; or two consecutive timeouts on two DIFFERENT URLs.
   A 401, 403, 404, 429, paywall, captcha or ROBOTS_DISALLOWED from a FETCHED SITE is a property
   of THAT SITE. Skip the URL, KEEP THE TOOL. Cloudflare returns 403 to bots constantly and
   killing WebFetch over one would end the run in ten minutes. NEVER RETRY AFTER A 402.
B) REJECTED vs UNREADABLE. Rejected means you OPENED the page and it failed a filter — a real
   result. Unreadable means no tier of the chain returned anything — a tooling failure in
   disguise. Separate tallies, with URLs. If unreadable exceeds 25 percent of pages attempted,
   open the report IN CAPITALS with "TOOLING DEGRADED: N of M pages could not be read. This is a
   FAILED RUN, not a thin day."
C) A RESEARCH TOOL FAILING IS NOT A STOP CONDITION. Fall down the chain and finish.

=== TARGET: 25 DRAFTS. FLOOR: 15. ===
FOLLOW-UPS COME FIRST, up to 5. New first-touch emails take the remainder, so 20 on a normal day.
Follow-ups are cheap, need no research, and are where replies actually come from. IF THE RUN RUNS
SHORT IT CUTS NEW COMPANIES AND NEVER CUTS FOLLOW-UPS.

Do not build a warm-up ladder that computes a tier from a count of distinct sending dates. Faisal
set 25 directly on 17 August; the ladder contradicts that and was a source of bugs on its own.

THE DOMAIN IS NOW AT ITS CEILING WITH NO HEADROOM. Task 3 runs two hours later from the same
address and takes up to 15, so 25 + 15 = 40 against a 40-per-day domain maximum. Exactly 40, not
27 as before. You do not need to account for the other task — stay inside your own 25 and the
arithmetic holds. But because there is no slack left, TWO THINGS BECOME MANDATORY RATHER THAN
NICE TO HAVE:

  1. NEVER CREATE A 26TH DRAFT, for any reason, including "one address was so good it seemed
     worth it". Over-running here silently steals Task 3's allocation two hours later.
  2. REPORT THE BOUNCE ARITHMETIC EVERY RUN (see the report section). At 40 sends a day on a
     domain this new, a bounce rate above 2 percent is an early warning that the domain is being
     scored as bulk. That is the number that decides whether this volume is sustainable, and
     nobody can see it unless the run prints it.

25 is a target, not a quota. THE FLOOR IS 15. Delivering 17 real, verified, personally-addressed
drafts is a good morning. Delivering 25 by relaxing anything is a bad one.

=== BUDGET: PLANNED 280 TOOL CALLS, ABSOLUTE CEILING 340 ===
RAISED AGAIN ON 18 AUGUST. Faisal's instruction, verbatim in effect: reaching the number matters,
and extra calls are authorised to reach it. THE EXTRA CALLS BUY MORE SOURCING LANES, NOT A LOWER
EVIDENCE BAR. Nothing in the verification rules moves.
Raised from 180/225 on 17 August, alongside the target going from 20 to 25. The arithmetic: about
eight to nine calls go into each *delivered* new draft once rejected candidates are counted, and
the target went from 15 new companies to 20. Leaving the budget at 180 would have produced a run
that systematically ran out at draft eighteen and reported a failure that was really an
under-resourcing. That exact mistake was made once already, on Task 3's original 70-call budget.

Work to 280. Spend it in this order so running out never costs the most valuable work:
~20 for the preflight, the reads and the exclusion sets; ~25 for the follow-ups; the remainder on
sourcing and email verification; and TEN CALLS HELD BACK, ALWAYS, for the audit and the
suppression-list write.

If you reach 280 and are STILL SHORT OF 25 DRAFTS you may continue to 340 — but only on calls
that will plausibly close the gap: sourcing a candidate, verifying an address, creating a draft.
NOT on retrying something that already failed, not on re-reading a page, not on a line of enquiry
that has produced nothing. 340 IS ABSOLUTE AND IS NEVER CROSSED FOR ANY REASON. Keep the ten-call
reserve either way.

*** THE OVERRUN BUYS MORE WORK, NEVER A LOWER BAR. *** It does not permit a guessed address, an
unverified claim, a relaxed filter, a shortened audit, or a shared inbox waved through. If 25
cannot be reached without lowering the evidence bar, DELIVER SHORT AND SAY SO — that is a correct
outcome and the entire reason this pipeline is worth running. Twenty-five drafts where two
addresses were invented is worse than eleven where none were.
Report the planned budget, the actual count, and any overrun with a one-line reason. IF YOU
OVERRUN THREE DAYS RUNNING, SAY SO PLAINLY — that means the target or the method needs
revisiting, not that the budget should quietly creep upward.

=== SUBAGENT POLICY — the single biggest cost in the run ===
Measured 13 August: two research subagents burned 197,000 and 113,000 tokens, and almost all of
it was them writing long prose reports back. Not prompt length. Not pages read. THE REPORTS.
  - No subagent for work doable in under 10 calls yourself.
  - AT MOST 2 RUNNING AT ANY ONE TIME (the container has two cores). THIS IS A CONCURRENCY CAP,
    NOT A TOTAL. There is no limit on how many you may spawn over the whole run, as long as never
    more than two are alive at once. On 17 August a run spawned two, got a thin result back, and
    concluded "I have used my 2 allowed subagents" — then stopped sourcing entirely and delivered
    7 drafts against a target of 25. THAT READING IS WRONG. Spawn the next pair.
  - DO NOT SPEND BOTH ON THE SAME LANE. Give each a DIFFERENT lane from the checklist in Step 3,
    so a thin result tells you something about that lane rather than about the day.
  - Every subagent gets its OWN HARD CALL BUDGET in its brief and reports the count it used.
  - Every subagent returns AT MOST 400 WORDS as NAMED STRUCTURED FIELDS. Essays, narrative,
    restating the brief and repeating itself are forbidden.
  - Keep briefs SHORT — every extra paragraph is re-sent on each of that agent's tool calls, so
    brief length multiplies by 60 to 70.

=== THE FIVE RULES THAT MATTER MORE THAN OUTPUT ===
1. ONE COMPANY GETS ONE FIRST-TOUCH EMAIL, EVER. A duplicate destroys the only asset this
   pipeline has.
2. NEVER INVENT AN EMAIL ADDRESS. Not from a pattern, not from a guess, not because it looks
   right. If it was not seen published on a page you actually OPENED, REJECT THE COMPANY. A
   rejected company is a correct outcome; a fabricated address is a bounce, and bounces damage
   the sending domain permanently. "The pattern is obvious from their other addresses" is not
   evidence. Neither is "most companies use firstname@". Reporting screened 90, found 4 is a good
   day. Reporting 5 where 2 were guessed is a disaster that shows up a week later.
3. ONE FOLLOW-UP PER PERSON, EVER. Then that person is finished forever. No second follow-up, no
   sequence.
4. NEVER FOLLOW UP ON A THREAD THAT HAS A GENUINE HUMAN REPLY IN IT, including a polite no.
5. NEVER SEND. Drafts only.

=== WHO FAISAL IS — sounds trivial, is not ===
He sends from TWO addresses and both are him: mehrfaisal111@gmail.com and faisal@faisalhanif.work
A message in a thread is from Faisal IF AND ONLY IF its sender address is one of those two,
case-insensitively.

*** NEVER MATCH ON THE STRING "FAISAL". *** The suppression list contains a DIFFERENT person —
Faisal Ilaiwi at faisal@intunedhq.com — and a name match would mark live leads as replied,
permanently, with no error and no way to notice.

create_draft has NO sender parameter. Drafts go from whatever Faisal has set as his Gmail default
sending address, confirmed 12 August as faisal@faisalhanif.work. You cannot set this and cannot
verify it from inside the session, so do not attempt workarounds and NEVER put a "From:" line in
the body.

=== STEP 1 — READ THE SUPPRESSION LIST WITHOUT CORRUPTING IT ===
state/do-not-contact.md is authoritative: ~256 rows in a pipe table plus prose sections carrying
the project's memory. Seven columns in THIS EXACT ORDER:

    | company_domain | email_domain | company | person | email | date | status |

A correct row:
| examplestartup.dev | examplestartup.dev | Example Startup | Jane Doe | jane@examplestartup.dev | 2026-08-18 | drafted |

(That row is a shape illustration only. Do not copy any part of it into the file.)

company_domain COMES FIRST. An earlier version listed ten fields in a different order; writing
that would have put person names into the domain column and built the next morning's duplicate
protection out of garbage. NEVER WIDEN THE TABLE — extra evidence URLs go in a separate
"## Source URLs" section underneath it.

PARSE ONLY THE PIPE ROWS UNDER THE HEADING "## The list". The file also contains a section headed
"Verified but NOT contacted — safe to use, do not block", and a whole-file regex scan would
wrongly block every address in it.

From those rows build THREE SETS:
  - blocked emails   = column 5, lowercased
  - blocked people   = column 4, lowercased
  - blocked domains  = column 1 for EVERY row always, PLUS column 2 but ONLY when that cell does
                       NOT contain the token "(freemail)"

*** THE FREEMAIL RULE. BOTH WAYS OF GETTING IT WRONG ARE INVISIBLE. ***
The marker sits inside the email_domain CELL, e.g.
| graphify.com | gmail.com (freemail) | Graphify Labs | Safi Shamsi | safishamsi98@gmail.com | 2026-08-02 | sent |
It applies to THAT CELL ONLY, never to the row. So graphify.com DOES go into blocked domains,
gmail.com NEVER does, and the email still does. Strip the marker before comparing.
Block gmail.com as a domain and you silently reject every future founder using a personal Gmail.
Skip the whole row and you silently UN-BLOCK fourteen companies contacted days ago.

*** STATUS IS AN "ALL" TEST, NOT A "CONTAINS" TEST. ***
Split the cell on commas, ignore case and bracketed text. A person is contactable ONLY IF EVERY
TOKEN is `drafted` or `sent`. If even one token is anything else, that person is PERMANENTLY
BLOCKED — no new email and no follow-up.
Measured 13 August: 256 rows, 8 compound — five `sent, FOLLOWED_1_DRAFTED`, one `sent, SEQUENCE_DONE`,
one `sent, REPLIED (declined, in-person only)`, one `sent, REPLIED (declined)`, plus five
single-token `BOUNCED`. A test asking whether the status CONTAINS "sent" passes all eight, which
would have sent a second follow-up to five founders and re-emailed Christophe Kafrouni at
zentio.ai — the one person who had actually replied.
THE SAME ALL-TOKENS TEST GOVERNS FOLLOW-UP ELIGIBILITY, not just new contact.
Vocabulary: drafted, sent, FOLLOWED_1, FOLLOWED_1_DRAFTED, SEQUENCE_DONE, REPLIED, BOUNCED,
OPTOUT. ONLY THE FIRST TWO PERMIT FUTURE CONTACT. FOLLOWED_1 and FOLLOWED_1_DRAFTED both mean
finished.

WIDEN THE NET WITH GMAIL, because a file goes stale: search `in:sent newer_than:60d` WITH
PAGINATION, and list drafts with the full view, paginated, adding every recipient to blocked
emails. DRAFTS COUNT AS CONTACTS — Faisal sends by hand over several days, so an unsent draft is
a contact about to happen. KEEP THE 60-DAY BOUND: an unbounded `in:sent` is dozens of calls
against a mailbox holding eleven thousand messages and would burn the run before any work
started. The table covers the older history.

PRINT THE THREE SET SIZES AND THE TABLE ROW COUNT IN YOUR REPORT. That is the proof the duplicate
protection actually ran.

MATCH ON DOMAIN, NEVER ON COMPANY NAME. Names rebrand — the same startup appears as "Context",
"Context.dev" and "context dev" — and a company's website domain and email domain are frequently
different: thirteen of the first sixty-six were, one being a site at tryscott.ai with email at
withjuno.dev. CHECK BOTH. Reject a candidate if its company domain, its email domain OR its email
address is blocked. A PERSON-NAME MATCH IS ONLY A REJECTION WHEN THE EMAIL DOMAIN MATCHES THAT
SAME ROW'S DOMAIN AS WELL — a name match alone is never sufficient, for the Faisal Ilaiwi reason.

=== STEP 2 — THE FOLLOW-UPS, WHICH COME FIRST ===
*** THE EXCLUSION SETS DO NOT APPLY HERE. *** This is counterintuitive enough that a careful run
gets it wrong. Blocked emails, people and domains exist to prevent a second FIRST TOUCH. Every
follow-up target is in blocked emails BY DEFINITION — that is the entire point of following up.
Applying the sets here would reject 100 percent of candidates and produce a silent zero-follow-up
day that looks exactly like a drained backlog.

For follow-ups the ONLY gates are: every status token is `sent` or `drafted`; exactly ONE message
in the thread; NO human reply; at least THREE DAYS old; and not already FOLLOWED_1.

Find them with search_threads on `in:sent older_than:3d newer_than:120d`, pageSize 50, and
*** PAGINATE FULLY WITH THE pageToken UNTIL THERE ARE NO MORE PAGES. *** Do not skip this.
pageSize defaults to 20 and THE FIRST PAGE IS THE NEWEST THREADS — precisely the ones you do not
want — so without pagination "take the five oldest eligible" is literally unreachable and the
backlog never drains. The 120-day bound only keeps the call count sane; if fewer than five
eligible threads appear inside it, widen to 180 and say so. NEVER NARROW IT — an earlier 21-day
window silently abandoned the entire 1-7 August cohort once those dates aged out, making roughly
230 people permanently invisible.

search_threads does NOT return per-message ids or reliable per-message senders. For every
candidate thread call get_thread and read the individual messages, their ids and their senders
from that result. Reply detection is impossible without it, and so is getting a replyToMessageId.

CLASSIFYING WHAT YOU FIND:
  - Sender mailer-daemon@ or postmaster@, or an auto-reply / out-of-office, is NOT A REPLY. If it
    is a bounce, mark the person BOUNCED and skip. Never report it as a reply — Faisal has had
    five bounces and one out-of-office already.
  - Any message from a REAL HUMAN who is not one of his two addresses means REPLIED: skip
    forever, mark it, and SURFACE IT PROMINENTLY IN THE REPORT. A real reply is the single most
    valuable thing this pipeline can find.
  - Exactly one message, from Faisal, three or more days old = ELIGIBLE.
  - Two or more messages from Faisal = the sequence is finished. Mark SEQUENCE_DONE, never touch
    it again.
COMPUTE AGE FROM THE MESSAGE DATE, not from the query — Gmail's date operators match messages and
whole threads leak through.

ONE FILTER EASY TO MISS: `in:sent` also returns job applications, personal mail and vendor mail.
A thread is only eligible if THE RECIPIENT ADDRESS APPEARS IN THE SUPPRESSION TABLE with a
passing status. Without that check you will eventually send a founder template with an invented
<Company> to one of Faisal's friends.

THERE IS NO UPPER AGE LIMIT. Roughly 230 people contacted between 1 and 7 August have never been
followed up; an eight-day ceiling would abandon nearly all of them. TAKE THE FIVE OLDEST
ELIGIBLE. The backlog drains at five a day, and FOLLOWED_1 is what marks someone done, not age.

THE DRAFT: create_draft with the recipient as an ARRAY OF BARE ADDRESSES — "Name <addr>" is NOT
supported and the call fails. Subject is "Re: " plus the original. Set replyToMessageId to the id
of the original message from get_thread. There is NO threadId parameter and NO from parameter.
replyToMessageId causes the original body to be appended, which is what you want — it gives the
founder the context of what they are answering.

THE FOLLOW-UP COPY IS FIXED. Only FIRSTNAME and COMPANY change. Nothing may be added or removed:

<div>Hi FIRSTNAME,</div><div><br></div><div>Bringing this back up once in case it got buried.</div><div><br></div><div>One question so I am not taking your time: are you adding engineers at COMPANY right now, or is it too early?</div><div><br></div><div>If it is not the right moment, no problem at all and I will leave it there.</div><div><br></div><div>Regards,</div><div>Faisal Hanif</div>

WHY IT READS THIS WAY, so nobody "improves" it later. It is three lines deliberately, because a
long follow-up reads as pressure. The word "once" tells the founder this is not a sequence — that
single word is the difference between a reminder and a campaign. "So I am not taking your time"
puts the cost on Faisal rather than the reader. The question is BINARY because open invitations
get ignored while yes-or-no questions get answered, and "it is too early" is an easy, face-saving
thing to type. And the closing line states plainly that this is the last message. THAT IS EXACTLY
WHY PEOPLE ANSWER IT, and it makes the one-follow-up rule an honest promise to the reader rather
than an internal policy nobody outside can see. THAT LINE MUST NEVER BE REMOVED.
NO PORTFOLIO LINK IN THE FOLLOW-UP — it is already in the message directly below it in the
thread, and repeating it makes the email look automated.

INSERT ALL OF THIS WITH CODE. Do not let a writing agent regenerate, extend, soften or improve
any of it, and NEVER paste a plain-text version into htmlBody — HTML ignores line breaks and it
would arrive as one run-on paragraph.

THEN WRITE THE SUPPRESSION LIST IMMEDIATELY, before starting on new companies. Do not hold status
changes in memory until the end — if the run dies during research there would be drafts sitting
in Gmail that the record knows nothing about.

=== STEP 3 — FINDING NEW COMPANIES ===

*** THE EIGHT LANES. YOU MAY NOT DECLARE A THIN DAY UNTIL ALL EIGHT HAVE BEEN ATTEMPTED. ***

On 17 August this run used two subagents, made ONE direct sweep of its own, screened about 118
companies against a 230-call budget, and reported: "I have exhausted the productive research lanes
for today." It had not. It had tried two of them and stopped, and Faisal got 2 new companies
instead of 20.

The rule that allowed it is further down this file and it is correct in itself: if 25 cannot be
reached without lowering the evidence bar, deliver short and say so. WHAT WAS MISSING IS HOW MUCH
WORK MUST HAPPEN BEFORE THAT CONCLUSION IS AVAILABLE. Here it is:

  LANE 1  YC company pages and YC launch posts
  LANE 2  HN "Who is hiring" — THIS month AND last month, both threads
  LANE 3  Greenhouse / Lever / Ashby / Workable API slug sweeps
  LANE 4  Funding news from the last 14 days. HIGHEST-YIELD LANE IN THIS PIPELINE — every
          personal address found on 7 August came from a "Media contact: Name, email" line in a
          press release, while /contact and /impressum pages produced almost nothing but info@.
          DO NOT SKIP THIS ONE.
  LANE 5  npm and PyPI maintainer records
  LANE 6  Public git commit author headers. Test ONCE (see the note further down); if it works it
          produced ten of twenty-six addresses on 7 August.
  LANE 7  Wellfound, WeWorkRemotely, RemoteOK
  LANE 8  The "Verified but NOT contacted" and "Rejected with a reason worth keeping" sections of
          state/do-not-contact.md. SEVERAL ARE NEAR MISSES THAT ONE NEW FACT WOULD REINSTATE —
          Homie needs one address confirmed, MiM and Ounas Health and Docupath each need a
          headcount, FlexDesk and Nectar and Flex each need one piece of non-US remote evidence.
          These are the cheapest verified companies available and they are being ignored.

*** YOU MAY NOT REPORT A THIN DAY UNTIL ALL EIGHT LANES HAVE BEEN ATTEMPTED AND YOU HAVE SPENT AT
LEAST 200 CALLS. *** A lane that returns nothing is attempted. A lane you did not open is not.
If you are at 200 calls with all eight attempted and still short, THEN deliver short and say so —
that is the honest outcome the rule was written for.

REPORT EVERY LANE SEPARATELY: name, companies screened, companies verified. A lane that produces
nothing three runs running gets demoted with the date and the count, exactly like the job-search
task's source table. Without per-lane numbers nobody can tell a thin day from an unopened lane,
which is precisely what happened on 17 August.

WORK THE LANES IN PARALLEL WHERE YOU CAN, two subagents at a time, different lane each, spawning
the next pair as they return. See the subagent policy above — two at a time is a concurrency cap,
not a total.


Start from places where a small company is advertising a REMOTE engineering role. The listing
proves three things at once — the company exists, it needs engineers, and it accepts remote —
which makes the hardest filter free. This matters because the only reply this campaign ever
received was a founder saying they hire in person only, and before 7 August there was no remote
filter at all.

START FROM SOURCES THAT NEED NO SEARCH ENGINE. The public ATS APIs return structured JSON with
real posting dates and WebFetch reads them directly:
  Greenhouse  https://boards-api.greenhouse.io/v1/boards/{token}/jobs?content=true
              -> title, location, first_published
  Lever       https://api.lever.co/v0/postings/{token}?mode=json          -> createdAt
  Ashby       https://api.ashbyhq.com/posting-api/job-board/{token}
              -> the ONLY one carrying a structured isRemote boolean. Disproportionately useful.
  Workable    https://apply.workable.com/api/v1/widget/accounts/{token}?details=true
              -> published_on
{token} is the company slug from the board URL: jobs.lever.co/matchgroup -> matchgroup. A 404
only means that company uses a different ATS; move on without comment. ONE CALL RETURNS 50 TO 200
ROLES, so twenty deliberate slugs beat a hundred guessed ones — slug-guessing is exactly where a
run wastes its budget. Find slugs with WebSearch on site:job-boards.greenhouse.io,
site:jobs.lever.co, site:jobs.ashbyhq.com, site:apply.workable.com plus the keywords.

THE SAME PRINCIPLE APPLIES TO ADDRESSES. The npm and PyPI maintainer records at
https://registry.npmjs.org/{package} and https://pypi.org/pypi/{package}/json are plain JSON and
produced BOTH verified emails in the 13 August test. THAT IS THE PRIMARY LANE FOR EMAIL
DISCOVERY, NOT A FALLBACK. And https://hn.algolia.com/api/v1/search_by_date with tags=comment is
the only genuinely date-sorted source anywhere in this system.

THEN TIER EVERYTHING ELSE.
  Finding URLs:  WebSearch -> mcp__Exa__web_search_exa -> Apify rag-web-browser with the keywords
                 as the query.
  Reading a URL you already have: WebFetch -> mcp__Exa__web_fetch_exa (its parameter is `urls`
                 and takes an ARRAY, not `url`) -> Apify with the URL itself as the query, then
                 read the markdown out with get-dataset-items using the dataset id returned.

OTHER SOURCES, in rough order of past yield: Y Combinator's Work at a Startup remote roles, where
the company page also states team size and location so the headcount filter comes free; the
Hacker News "Ask HN: Who is hiring?" threads for the current and previous month searched for
remote, where founders of tiny companies routinely write "email me at x@company.com"; Wellfound
remote filtered to small teams; WeWorkRemotely and RemoteOK engineering, startups only; and
recent pre-seed / seed funding news followed by a check for a remote posting.
DO NOT USE remotive.com — it blocks the API in robots.txt. RemoteOK's /api is readable plain JSON
but heavily polluted with non-engineering and spam entries: filter hard and never trust its dates
over an ATS date.

EVERY COMPANY NEEDS A RECORDED remote_evidence_url. A live role advertised as remote, worldwide
or remote-friendly counts; so does a "remote-first" or "distributed team" statement on their own
site, or a team page showing people in different countries. "Hybrid" does NOT count. "Remote in
the US only" does NOT count. An assumption that a startup is probably fine with it does NOT
count. NO REMOTE EVIDENCE MEANS REJECT THE COMPANY.

ONE CASE THAT SLIPS PAST ALL OF THAT WORDING: a timezone band that excludes UTC+5. "Remote, GMT+1
to GMT-5" is neither hybrid nor US-only, so it reads as acceptable, but Faisal cannot take it.
REJECT IT and log it as "timezone band excludes UTC+5".

HARD FILTERS:
  - Headcount 1 to 15 WITH A STATED SOURCE.
  - HQ in the USA, UK, or Europe including the EEA and Switzerland.
  - A real software product — NOT an agency, dev shop, consultancy or staffing firm.
  - Work in web, mobile, cloud, backend or AI. Excludes pure hardware and wet-lab biotech.
  - A NAMED TECHNICAL DECISION-MAKER: founder, co-founder, CEO, CTO, head of engineering, VP
    engineering, engineering manager, technical lead or founding engineer.

BE SPECIFIC ABOUT HEADCOUNT so two runs are comparable. A number stated on a page you opened
counts — YC's "Team Size: 6", an about page saying "we are 9". An exhaustive named roster on the
company's own team page also counts: count the names. "We're a small team", "a handful of us",
and any crawler or broker estimate DO NOT COUNT. Say which of the two you used.

=== STEP 4 — VERIFYING THE ADDRESS ===
ONLY an address seen published on a page you actually OPENED, with the URL recorded. NEVER
constructed from a pattern — not firstname@, not first.last@, not initial-plus-lastname, NEVER.
If no published address can be found, REJECT THE COMPANY.

DISTINGUISH "I opened the pages and there was no address" from "I could not open the pages at
all". The second is UNREADABLE, not rejected, and goes in the separate tally. Letting a tooling
failure be reported as "rejected for no published address" is the exact disguise a broken run
wears.

REJECT rather than use these prefixes:
  careers@ jobs@ recruiting@ recruitment@ hr@ apply@ support@ help@ helpdesk@ noreply@ no-reply@
  admin@ billing@ press@ media@ legal@ security@ abuse@ webmaster@

SHARED INBOXES — founders@ contact@ team@ hello@ hi@ info@ — are ALSO a rejection here. Every
bounce this campaign has ever had came from a shared inbox, and no personal address published for
a named person has ever bounced; the 7 August run hit 26 personal addresses out of 26, so 100
percent personal is the proven standard rather than an aspiration.
BUT when a company passes every other filter and dies ONLY on this, list it in the report under
"NEAR MISS — shared inbox only" WITH THE ADDRESS, so Faisal can decide by hand. On 13 August that
would have surfaced Plausible Analytics: a team of ten stated on their own page, "Location:
Remote (worldwide)" verbatim, based in Estonia, a real open-source product, killed solely because
the only published addresses were jobs@ and hello@.

LOOK IN THIS ORDER, which is the order that actually produced results:
  1. npm and PyPI maintainer records — BOTH verified emails in the 13 August test came from here.
  2. The company's own about, team and contact pages, the footer, blog author bylines, and
     /impressum or /legal, which EU and German sites are legally required to publish.
  3. The founder's personal site, conference speaker pages, podcast notes, press releases.
  4. YC launch posts, which often end with "contact us at name@company.com".

ONE THING TO TEST RATHER THAN ASSUME: GITHUB COMMIT HEADERS. When it works this is the single
best source for open-source founders — ten of the twenty-six addresses found on 7 August came
from it. Fetch https://api.github.com/repos/OWNER/REPO/commits and read the author email, or open
a commit as a .patch URL. Skip anything ending users.noreply.github.com.
BUT in the PREVIOUS environment both api.github.com and github.com returned "GitHub access to
this repository is not enabled for this session" and the atom feeds were ROBOTS_DISALLOWED. This
environment is different and may well allow it. TEST IT ONCE, note the result under tool health,
and move on either way. Do not keep retrying if it fails.

RECORD for each address: the source URL, a one-line note on how it appeared, and a confidence of
HIGH (published for that exact person) or MEDIUM (a company address at a tiny team that clearly
reaches them). THERE IS NO GUESSED TIER.

=== STEP 5 — HOW THE EMAIL HAS TO SOUND ===
Reference version, and the shape is doing real work:

  Subject: Onlook and the design-to-code gap

  Hi Daniel,

  I went through what you are building at Onlook. Letting designers edit the real
  running app on canvas and having every change land back in the codebase is the
  version of that handoff that actually works, and it is a hard thing to get right.

  I work across full-stack development, system design, software architecture and
  cloud infrastructure, building the product itself and the parts that decide
  whether it holds up as usage grows. 3+ years shipping production systems on web
  and mobile: PureBody, an AI fitness app with 5,000 users across Google Play and
  the App Store, and UHA International, an enterprise platform built for a client.

  I would be glad to contribute to what you are building at Onlook, working
  remotely. Are you adding engineers right now, or is it too early?

  Regards,
  Faisal Hanif
  faisalhanif.work

THE MIDDLE PARAGRAPH — the positioning — IS IDENTICAL IN EVERY EMAIL, WORD FOR WORD, and must be
inserted WITH CODE rather than regenerated. It leads with heavy general skills because those
attract more interest than naming frameworks, and for that reason THE EMAIL MUST NEVER LIST
React, Next.js, Node, TypeScript, AWS or any other framework or language. Do not put a URL for
UHA International in the body; naming it is enough.

THE CLOSING TWO SENTENCES ARE ALSO FIXED, with only the company name varying. Three things in
them are load-bearing and all three are required: naming the company stops it reading as a mass
mail; "working remotely" states the arrangement so nobody has to guess whether he wants to
relocate; and ending on a yes-or-no question gets an answer where an open invitation gets
silence.

WHAT VARIES PER COMPANY IS ONLY:
  - the SUBJECT: four to seven words about what they build, NO domain name in it
  - the OPENING: 35 to 55 words that start by saying he went through their work, then say what
    they are building and why it is worth doing.
*** THE OPENING IS NOT A CRITIQUE. *** It must never point out flaws or stale pages. An earlier
version did that and Faisal rejected it.

FORBIDDEN WORDS ANYWHERE IN THE EMAIL:
  looking for opportunities, seeking, open to work, available, hire me, please consider, kindly,
  apply, application, position, vacancy, free, no cost, volunteer, unpaid, trial, discounted,
  rate, salary, passionate, dedicated, hardworking, team player
  plus "I am writing to" and "I came across your company".
No em dashes, no emoji, no exclamation marks, no bold, no bullet points, and NO domain or URL
anywhere except faisalhanif.work once in the sign-off. NO HYPHEN — faisal-hanif.work is dead and
must never be used.

RUN THE FORBIDDEN-WORD CHECK AS A SUBSTRING MATCH, BUT MASK COMPANY AND PERSON NAMES FIRST,
because "Sentrial" contains trial, "iterate" and "accurate" contain rate, and "strong position"
contains position.

WHEN CREATING THE DRAFT pass ONLY `to`, `subject` and `htmlBody`. *** NEVER PASS `body`. *** A
plain-text body makes Gmail rewrite every bare domain into a google.com/url tracking string that
displays as forty characters of garbage where the portfolio link should be. That happened once,
sixty-six drafts had to be deleted, and Faisal was rightly unhappy.
Wrap the portfolio in a real anchor: <a href="https://faisalhanif.work">faisalhanif.work</a>
One <div> per paragraph and <div><br></div> between them.

=== STEP 6 — WRITE THE SUPPRESSION LIST ===
Append today's rows to state/do-not-contact.md under "## The list", in the seven-column order
above. You have git, so APPEND — do not rewrite the file.

WRITE WHAT ACTUALLY HAPPENED, NOT WHAT WAS INTENDED. An audit on 13 August found drift in BOTH
directions: 26 rows dated 7 August still reading `drafted` when Gmail showed all 26 in Sent, and
rows reading `sent, FOLLOWED_1_DRAFTED` whose follow-ups may still be unsent drafts (10 today).
DO NOT PROMOTE A DRAFT TO `sent`. Use FOLLOWED_1_DRAFTED when the follow-up is only drafted, and
say so in the report.

COUNT THE ROWS BEFORE AND AFTER. After must be before plus the number of rows you added. If it is
lower you dropped rows: do not commit, rebuild once, and if the second attempt is still short DO
NOT COMMIT AT ALL and open the report IN CAPITALS listing every draft created today with
recipient, company and address, under a heading saying the suppression list was not updated and
the task must not run again until those rows are added by hand. A BARE STOP IS NOT ENOUGH — the
drafts already exist in Gmail.


*** THE RUN NEVER COMMITS TO MAIN. IT OPENS A PULL REQUEST. ***

Faisal's instruction, 18 August: every run must leave a pull request he can read and merge, so he
can see what was drafted, who was contacted, and what state changed, before any of it becomes the
record. Direct pushes to `main` are finished.

**The branch name is fixed:**

```
run/task-1-{YYYY-MM-DD}          e.g. run/task-1-2026-08-19
```

*** STEP A — BEFORE READING ANY STATE, CHECK FOR UNMERGED RUN BRANCHES. ***

This is the failure mode a PR workflow creates and it will bite silently if you skip it. If
yesterday's PR is still open, `main` does not contain yesterday's rows, and a run that branches
from `main` will re-contact everyone yesterday drafted.

```
git fetch --all --prune
git branch -r --no-merged origin/main | grep 'origin/run/'
```

  - **Nothing unmerged** -> branch from `origin/main` as normal.
  - **One or more unmerged run branches** -> **BRANCH FROM THE MOST RECENT ONE, NOT FROM MAIN**,
    and read every state file from it. State chains forward whether or not Faisal has merged yet.
    Then open the report IN CAPITALS with:
    "N UNMERGED RUN BRANCHES: <names>. TODAY BRANCHED FROM <branch> SO STATE IS CORRECT, BUT
    MERGE THEM OR THE CHAIN KEEPS GROWING."
  - Say in the report which branch you based on, every run, without exception.

*** STEP B — PUSH THE BRANCH EARLY AND MORE THAN ONCE. ***

Push after the first state write, before the expensive research starts. Push again after each
later write. A run that dies at call 250 should already have its first push on the remote.
**After every push, verify it landed:** `git ls-remote origin run/task-1-{DATE}` and compare the
SHA to local HEAD. A clean exit code is not proof; a matching SHA is.

*** STEP C — OPEN THE PULL REQUEST. ***

Try in this order and stop at the first that works:

  1. `gh pr create --base main --head run/task-1-{DATE} --title "..." --body "..."`
  2. The GitHub MCP `create_pull_request` tool, if present.
  3. If both fail but the branch pushed: report the compare URL
     `https://github.com/FaisalHanif12/outreach-schedule/compare/main...run/task-1-{DATE}`
     so Faisal can open the PR in two clicks. **A pushed branch with no PR is a degraded success,
     not a failure** — the rows are safe on the remote.

**PR title:** `task-1 {DATE}: N drafts, M state rows`

**PR body — these sections, in this order, every time:**

```
## Numbers
target / delivered / floor, and the split

## Deliverability
bounces last 24h, bounce rate, replies

## Contact ledger  (the two-touch invariant)
rows at 1 touch  (drafted or sent, eligible for one follow-up)   : N
rows at 2 touches (FOLLOWED_1 or FOLLOWED_1_DRAFTED, finished)   : N
rows closed by REPLIED / BOUNCED / OPTOUT / SEQUENCE_DONE        : N
rows that would exceed 2 touches                                 : MUST BE 0

## Who was contacted today
one line each: company, person, address, first touch or follow-up

## State changes
rows added, rows edited and from what to what, row count before -> after

## Anything that needs a decision
```

*** THE TWO-TOUCH INVARIANT. CHECK IT BEFORE EVERY WRITE. ***

**No person and no company ever receives more than two messages: one first touch, one follow-up.
That is the whole rule and it is the point of the tracker.**

Count touches from the status cell:

```
drafted | sent                            = 1 touch   -> one follow-up still allowed
FOLLOWED_1 | FOLLOWED_1_DRAFTED           = 2 touches -> FINISHED
SEQUENCE_DONE                             = 2 or more -> FINISHED
REPLIED | BOUNCED | OPTOUT                = closed regardless of count
```

Before writing any row, compute what its touch count becomes. **If any row would reach 3, that is
a bug in the run, not a decision to make.** Do not write it, do not create the draft, and open the
report in capitals naming the row. This has never happened and it must stay that way.

*** IF NOTHING PUSHES AT ALL, THE RUN HAS FAILED. ***

Not "succeeded with a caveat". Failed.

  a) Do not retry more than twice. A 403 is a permission fact, not a network blip. On 17 August
     two independent credentials failed identically all day and retrying changed nothing.
  b) **Send the FULL updated state file as a file**, not just the report. The report is not the
     state. On 17 August Task 3 sent its tracker and 22 rows survived; Task 1 sent only its report
     and its suppression-list update was lost with the container.
  c) Open the report IN CAPITALS with:
     "STATE WRITE DID NOT LAND. DO NOT TRIGGER THE NEXT RUN UNTIL THIS IS PUSHED — IT WILL
     RE-CONTACT PEOPLE DRAFTED TODAY."
  d) List every row added or changed in full table syntax, so it can be pasted by hand.

=== STEP 7 — CHECK YOUR OWN WORK ===
Confirm the expected number of drafts exists; that no first-touch recipient from today appears in
the blocked set or twice in today's own list; that every follow-up carries a replyToMessageId and
a "Re: " subject; and that every recipient and subject is as intended.
DO THIS AGAINST THE SETS YOU ALREADY BUILT, not by running a fresh unbounded Gmail search, which
is banned for the cost reason above.

THREE SPECIFICS:
  - DO NOT check for a `plaintextBody` field. list_drafts returns a plaintext rendering for every
    draft regardless of what was passed, so that check always fails and means nothing.
  - THE get_thread HTML CHECK USUALLY DOES NOT WORK AND IS NOT REQUIRED. Try it ONCE on one draft:
    get_thread with messageFormat FULL_CONTENT (that argument is required; PLAIN_TEXT, MINIMAL and
    METADATA_ONLY all omit html_body and the check would falsely fail). On 17 August this returned
    a permission error on draft-only threads and list_drafts returned no body either. IF IT FAILS,
    NOTE IT UNDER TOOL HEALTH AND MOVE ON. Do not spend more than one call on it.
  - THE CHECK THAT ACTUALLY PROTECTS AGAINST THE google.com/url REWRITE IS STRUCTURAL, NOT
    OBSERVATIONAL: assert that EVERY create_draft call this run passed `htmlBody` and that NONE
    passed `body`. Gmail only rewrites links when a plain-text part is supplied, so if `body` was
    never passed the rewrite cannot happen. State that assertion explicitly in the report, with
    the count of drafts it covers.

=== STOP CONDITIONS ===
- Nothing pushed at all -> THE RUN HAS FAILED. Follow the block in step 6: send the state file,
  open the report in capitals, list every changed row. Do not report success.
- A row would reach a third touch -> STOP. Do not write it, do not draft it, report it.
- Could not read state/do-not-contact.md -> STOP. Without it the never-contact-twice rule cannot
  hold.
- The blocked-emails set came out below 80 percent of the row count you just measured -> the
  parse failed -> STOP.
- The row count you are about to write is lower than what you read -> STOP per step 6.
- A RESEARCH TOOL FAILING IS NOT A STOP CONDITION. Fall down the chain and finish.

=== STEP 8 — REPORT. Short, plain English, no em dashes. ===
Write it to daily/task-1-<YYYY-MM-DD>.md AND output it. In this order:
  a) The Sent-folder check result from step 0a
  b) The preflight block: which tools ALIVE, which DEAD with the exact error
  c) Row counts and the three set sizes
  d) Follow-ups, with ANYONE WHO REPLIED QUOTED IN FULL, and bounces found
  e) New companies: screened / unreadable / rejected for no remote evidence / rejected for no
     published address / drafts created / skipped as already contacted
  f) Shared-inbox NEAR MISSES with their addresses
  g) Which daily total you applied and the split, against the target of 25 and the floor of 15
  h) THE DELIVERABILITY BLOCK. Three numbers, every run, no exceptions:
       - bounces found in the inbox in the last 24 hours, and the addresses
       - bounce rate as a percentage of the last 100 rows marked sent in state/do-not-contact.md
       - replies received in the last 24 hours
     IF THE BOUNCE RATE IS ABOVE 2 PERCENT, open the whole report IN CAPITALS with
     "DELIVERABILITY WARNING: BOUNCE RATE N PERCENT. RECOMMEND PAUSING VOLUME." Do not change
     the target yourself — that is Faisal's decision — but make the number impossible to miss.
     At 40 sends a day across the two tasks the domain has no slack left, and a rising bounce
     rate is the only early signal that exists before mail starts landing in spam.
  i) Anything unusual you assumed
  j) Tool health
  k) Budget: total calls against the planned 280 and the absolute 340, the size of any overrun
     with a one-line reason, how many subagents were spawned and what each was given
Then commit and stop. Do not send anything.
