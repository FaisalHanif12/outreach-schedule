# DO NOT CONTACT

Authoritative suppression list for the founder outreach campaign (Task 1). **This file is the
only thing standing between Faisal and emailing the same founder twice.**

Migrated from the old document store on 17 August 2026. The rows are unchanged. What changed is
how it gets written: see "After every run" below.

> **This repository must stay private.** The table below is 259 real people with their real
> email addresses.

## How to use this file — every run, without exception

Before researching anything, read this file and build three blocked sets:

```
BLOCKED_DOMAINS - every value in company_domain, plus every value in email_domain
                  EXCEPT any marked (freemail). See TRAP 1.
BLOCKED_EMAILS  - every value in the email column, exactly
BLOCKED_PEOPLE  - every value in the person column, lowercased
```

Reject a candidate if **any** of these is true:

- its company website domain is in `BLOCKED_DOMAINS`
- the domain of its email is in `BLOCKED_DOMAINS`
- its email is in `BLOCKED_EMAILS`
- its person name is in `BLOCKED_PEOPLE` **and** its company domain also matches

## Two traps that will bite you

**TRAP 1 — NEVER block a freemail domain.**
Some founders use a personal Gmail as their work address. Those rows are marked `(freemail)` in
the `email_domain` column. Blocking `gmail.com`, `outlook.com` or `hey.com` as a domain would
silently reject every future founder who uses one, and you would never notice.
**For a `(freemail)` row, block the EXACT ADDRESS ONLY.** Never add that domain to
`BLOCKED_DOMAINS`.

The marker applies to **the cell it is in, not the row.** A row can have a real company domain and
a freemail email domain at the same time — block the first, not the second.

**TRAP 2 — Match on domain, never on company name.**
Company names are unreliable. The same startup appears as "Context", "Context.dev" and "context
dev" across sources, and companies rebrand. Domains are stable.

Also: a company's website domain and its email domain are **often different** — 13 of the first 66
were. Scott AI's site is `tryscott.ai` but its email is at `withjuno.dev`. Both are recorded and
**both must be checked.**

**And never match on the substring "Faisal".** Row `intunedhq.com` is **Faisal Ilaiwi**, a
different person and a real prospect contacted on 4 August. Match on exact email, on domain, and
on full lowercased name plus domain. Never on a fragment.

## Status is an ALL test, not a CONTAINS test

Statuses are compound: `sent, FOLLOWED_1_DRAFTED`, `sent, REPLIED (declined)`. A person is
contactable only if **every** comma-separated token permits contact.

Measured against this file on 13 August: 256 rows, 8 of them compound (259 rows and 18 compound
statuses today). A test
asking whether the status *contains* "sent" passes all eight — which would have sent a second
follow-up to five founders and re-emailed **Christophe Kafrouni at zentio.ai, the one person who
had actually replied.**

## One company, one email, ever

If a company was contacted through a shared inbox and you later find the founder's personal
address, **it is still blocked.** Do not "upgrade" a previous contact. Do not retry a bounce at a
different address unless Faisal explicitly asks.

## After every run — mandatory

**This file now lives in git, so append rows. Do not reproduce the whole file.** The old document
store replaced files wholesale with no append, which forced a byte-for-byte reproduction ritual
and still lost rows in both directions.

1. Count existing rows as **N**.
2. Append one row per person contacted.
3. Count again and confirm the total is **N + rows added**.
4. Commit, with the date and both counts in the message.

If the count comes out lower, **do not commit.** Rebuild once; if it is still short, do not commit
at all and report at the top of your output in capitals, **listing every draft created that day
with recipient and company** — because an unrecorded draft becomes a second first touch tomorrow.

A bad write now shows up in a diff instead of vanishing silently. That is the one thing this
migration bought.

## Status values

```
sent          - Faisal sent it
drafted       - a draft exists in Gmail, may be unsent. BLOCKS JUST AS HARD as "sent",
                because he sends by hand over several days and an unsent draft is a
                contact that is about to happen
FOLLOWED_1_DRAFTED - a follow-up draft exists, may be unsent. BLOCKS. The follow-up has
                already been written, so writing another is a duplicate.
FOLLOWED_1    - got the one and only follow-up. Finished. Never contact again.
SEQUENCE_DONE - two or more messages already sent by Faisal in the thread. Finished.
REPLIED       - a real human replied. Never contact again.
BOUNCED       - hard bounced. Never retry this address or this company.
OPTOUT        - asked not to be contacted. Never contact again, for any reason.
```

## RESOLVED — the auto-send incident, closed 6 August 2026

Between 4 and 6 August, emails left this account without Faisal pressing send. Roughly 50 went out
in a three minute window on 4 August, 27 more that evening, 30 on 5 August, and about 26 on
6 August. It produced five duplicate sends and two companies contacted twice at different
addresses.

**Cause:** his Gmail was connected to **Apollo.io** as a sending mailbox on 4 August at 01:18 UTC.
Apollo was the only connector on the account with a send capability. The Gmail connector cannot
send at all through drafts; it creates and updates them.

**Fix:** Faisal disconnected Apollo on 6 August, part-way through that day's sweep. Twenty-six of
the thirty drafts had already gone out between 12:30 and 12:37 UTC. The remaining four survived,
which is the proof the send path closed. Those four left at 20:54 UTC that evening, seven minutes
after Faisal manually typed and sent a reply to Chris Kafrouni at Zentio — consistent with him
clearing drafts by hand rather than another sweep.

Verified again by the 7 August run: the Drafts folder contained no outreach drafts before it
started, and every 6 August address appears exactly once in sent mail.

**This section is history, not an active warning.** It is kept because if mail ever starts leaving
this account again without him, **connected mailboxes are the first thing to check.** Note that
this is a *different* incident from the 14 August one described in the repo README — that one was
the run calling `send_message` itself.

## FIRST REPLY OF THE CAMPAIGN — 6 August 2026

Chris Kafrouni at Zentio replied on 6 August at 14:42 UTC. A polite decline: they were only hiring
for in-person roles. Faisal answered it himself at 20:47 UTC. That was the first reply, in roughly
230 contacts. Two more have followed: Storepass on 7 August (also a decline) and Hugentic on
14 August. **Three human replies in total.**

**The objection was location, not the pitch** — a filter problem rather than a copy problem.
Nothing in the sourcing at that point checked whether a company would consider remote. That is why
the remote-friendly signal is now a hard filter.

The 6 August emails also went out with an older positioning paragraph ("Four years shipping
production systems...") rather than the version Faisal approved on 5 August, and carried a
plain-text body alongside the HTML, which is why the portfolio link arrived as a `google.com/url`
string. Both fixed as of 7 August. **Never pass `body`.**

## The list

| company_domain | email_domain | company | person | email | date | status |
|---|---|---|---|---|---|---|
| airweave.ai | airweave.ai | Airweave | Lennert Jansen | lennert@airweave.ai | 2026-08-02 | sent, FOLLOWED_1_DRAFTED |
| ambral.com | ambral.com | Ambral | Sam Brickman | founders@ambral.com | 2026-08-02 | sent, FOLLOWED_1_DRAFTED |
| societies.io | societies.io | Artificial Societies | James He | founders@societies.io | 2026-08-02 | sent, FOLLOWED_1_DRAFTED |
| assistant-ui.com | assistant-ui.com | assistant-ui | Simon Farshid | hello@assistant-ui.com | 2026-08-02 | sent, FOLLOWED_1_DRAFTED |
| avrea.com | avrea.com | Avrea | Hannu Valtonen | hello@avrea.com | 2026-08-02 | BOUNCED |
| getbalance.ai | getbalance.ai | Balance | Gus Levinson | founders@getbalance.ai | 2026-08-02 | sent, FOLLOWED_1_DRAFTED |
| beam.cloud | beam.cloud | Beam | Eli Mernit | founders@beam.cloud | 2026-08-02 | sent |
| bloom.diy | bloom.diy | Bloom | David Oort Alonso | founders@bloom.diy | 2026-08-02 | sent |
| boundaryml.com | boundaryml.com | Boundary | Vaibhav Gupta | founders@boundaryml.com | 2026-08-02 | sent |
| claimhealth.com | claimhealth.ai | Claim Health | Kevin Calcado | kevin@claimhealth.ai | 2026-08-02 | sent |
| clutchapp.io | clutchapp.io | Clutch | Kári Gunnarsson | kari@clutchapp.io | 2026-08-02 | sent |
| combinely.ai | combinely.ai | Combinely | Tom Invernizzi | tom@combinely.ai | 2026-08-02 | sent |
| comena.ai | comena.ai | Comena | Jiehua Wu | jiehua.wu@comena.ai | 2026-08-02 | sent |
| complydo.io | complydo.io | ComplyDo | Leo Schuhmann | leo.schuhmann@complydo.io | 2026-08-02 | sent |
| context.dev | hey.com (freemail) | Context.dev | Yahia Bakour | bakour@hey.com | 2026-08-02 | sent |
| crimson.law | crimson.law | Crimson | Mark Feldner | careers@crimson.law | 2026-08-02 | sent |
| getdexter.co | getdexter.co | Dexter | Bella Wu | jobs@getdexter.co | 2026-08-02 | sent |
| floot.com | floot.com | Floot | Edward Look | hello@floot.com | 2026-08-02 | sent |
| graphify.com | gmail.com (freemail) | Graphify Labs | Safi Shamsi | safishamsi98@gmail.com | 2026-08-02 | sent |
| helix-db.com | helix-db.com | HelixDB | George Curtis | george@helix-db.com | 2026-08-02 | sent |
| heytelo.com | heytelo.com | Hey Telo | Christopher Grittner | info@heytelo.com | 2026-08-14 | sent, FOLLOWED_1_DRAFTED |
| hugentic.ai | hugentic.ai | Hugentic | Mark Bird | hello@hugentic.ai | 2026-08-13 | sent, REPLIED |
| hyperprobe.co | hypertest.co | HyperProbe | Karan Raina | karan@hypertest.co | 2026-08-02 | sent |
| ix.dev | ix.dev | Indexable | Andrew Gazelka | andrew@ix.dev | 2026-08-14 | sent, FOLLOWED_1_DRAFTED |
| inkbox.ai | inkbox.ai | Inkbox | Ray Liao | ray@inkbox.ai | 2026-08-14 | sent, FOLLOWED_1_DRAFTED |
| lim.run | lim.run | Limrun | Muvaffak Onuş | hello@lim.run | 2026-08-14 | sent, FOLLOWED_1_DRAFTED |
| meticulate.ai | meticulate.ai | Meticulate | Joseph Palakapilly | joseph@meticulate.ai | 2026-08-13 | sent, FOLLOWED_1_DRAFTED |
| moss.dev | usemoss.dev | Moss | Sri Raghu Malireddi | founders@usemoss.dev | 2026-08-13 | sent, FOLLOWED_1_DRAFTED |
| getnao.io | getnao.io | nao Labs | Claire Gouze | claire@getnao.io | 2026-08-14 | sent, FOLLOWED_1_DRAFTED |
| o11.ai | o11.ai | o11 | Aryah Oztanir | support@o11.ai | 2026-08-13 | sent, FOLLOWED_1_DRAFTED |
| onlook.com | onlook.com | Onlook | Daniel Farrell | daniel@onlook.com | 2026-08-13 | sent, FOLLOWED_1_DRAFTED |
| ooakdata.com | ooakdata.com | Ooak Data | Thomas Aubry | contact@ooakdata.com | 2026-08-02 | sent |
| theopenbuilder.com | theopenbuilder.com | OpenBuilder | James Jiang | james@theopenbuilder.com | 2026-08-02 | sent |
| orbio.earth | orbio.earth | Orbio Earth | Robert Huppertz | info@orbio.earth | 2026-08-02 | sent |
| orbit.do | orbit.do | Orbit | Philip John Mordecai | inquiry@orbit.do | 2026-08-02 | sent |
| otio.ai | otio.ai | Otio AI | Yasaman Rajaee | contact@otio.ai | 2026-08-02 | sent |
| palette.team | palette.team | Palette | Lars Ettrup | hello@palette.team | 2026-08-02 | sent |
| trypango.ai | pango.ai | Pango | Lukasz Reszczynski | lukasz@pango.ai | 2026-08-02 | sent |
| pangolin.net | pangolin.net | Pangolin | Milo Schwartz | careers@pangolin.net | 2026-08-02 | sent |
| prized.dev | prized.dev | Prized | Hudson Griffith | founders@prized.dev | 2026-08-02 | sent |
| tryreplicas.com | replicas.dev | Replicas | Connor Loi | connor@replicas.dev | 2026-08-02 | sent |
| rhizomeai.com | rhizomeai.com | Rhizome AI | Chetan Mishra | support@rhizomeai.com | 2026-08-02 | sent |
| tryrobby.com | tryrobby.com | Robby | Vineet Jammalamadaka | founders@tryrobby.com | 2026-08-02 | sent |
| runtm.com | runtm.com | Runtime | Carlos Volante | carlos@runtm.com | 2026-08-02 | sent |
| tryscott.ai | withjuno.dev | Scott AI | David Maulick | founders@withjuno.dev | 2026-08-02 | sent |
| screenpipe.com | screenpi.pe | Screenpipe | Louis Beaumont | louis@screenpi.pe | 2026-08-02 | sent |
| sembleai.com | sembleai.com | Semble AI | Ethan Boyers | info@sembleai.com | 2026-08-02 | sent |
| sitefire.ai | sitefire.ai | Sitefire | Jochen Madler | info@sitefire.ai | 2026-08-02 | sent |
| specific.dev | flapplabs.se | Specific | Fabian Lindfors | fabian@flapplabs.se | 2026-08-02 | sent |
| spiral.ad | spiral.ad | Spiral | Filip Knyszewski | founders@spiral.ad | 2026-08-02 | sent |
| squid.energy | squid.energy | Squid Energy | Conor Jones | hello@squid.energy | 2026-08-02 | sent |
| stilta.com | stilta.com | Stilta | Oskar Block | oskar@stilta.com | 2026-08-02 | sent |
| superset.sh | superset.sh | Superset | Kiet Ho | hello@superset.sh | 2026-08-02 | sent |
| tasklet.ai | tasklet.ai | Tasklet | Andrew Lee | andrew@tasklet.ai | 2026-08-02 | sent |
| telmi.io | telmi.io | telmi | Véronique Trang | vero@telmi.io | 2026-08-02 | sent |
| templecompute.com | gmail.com (freemail) | Temple Compute | Christian Dominguez Dalmases | cdominguezdalmases@gmail.com | 2026-08-02 | sent |
| theforecastingcompany.com | polytechnique.edu | The Forecasting Company | Geoffrey Negiar | geoffrey.negiar@polytechnique.edu | 2026-08-02 | BOUNCED |
| tradepolaris.com | tradepolaris.com | TradePolaris | Rohan Rathod | r@tradepolaris.com | 2026-08-02 | sent |
| trytrata.com | trata.com | Trata | Eric Cho | eric@trata.com | 2026-08-02 | sent |
| unsiloed.ai | unsiloed.ai | Unsiloed AI | Adnan Abbas | founders@unsiloed.ai | 2026-08-02 | sent |
| wayline.com | wayline.com | Wayline | Jason Okra | founders@wayline.com | 2026-08-02 | sent |
| whitespacehq.ai | whitespacehq.ai | Whitespace | Alex Tung | alex@whitespacehq.ai | 2026-08-02 | sent |
| windmill.dev | windmill.dev | Windmill | Ruben Fiszel | ruben@windmill.dev | 2026-08-02 | sent |
| wolfia.com | wolfia.com | Wolfia | Naren Manoharan | naren@wolfia.com | 2026-08-02 | sent |
| zalos.ai | zalos.ai | Zalos | William Fairbairn | will@zalos.ai | 2026-08-02 | sent |
| zaplar.com | zaplar.com | Zaplar | Axel Andersson Lingbert | founders@zaplar.com | 2026-08-02 | sent |
| able.global | able.global | able.global | Alexandra Wright | aw@able.global | 2026-08-04 | sent |
| aglide.com | aglide.com | Aglide | Patrick D. McGuckian | p@aglide.com | 2026-08-04 | sent |
| ai-baseline.com | ai-baseline.com | AI Baseline | Xenia Galkina | xenia.g@ai-baseline.com | 2026-08-04 | sent |
| artifact.engineer | artifact.engineer | Artifact | Antony Samuel | antony@artifact.engineer | 2026-08-04 | sent |
| banani.co | banani.co | Banani AI | Vlad Solomakha | vlad@banani.co | 2026-08-04 | sent |
| booma.ai | booma.ai | Booma | Kareem Bayoun | kareem@booma.ai | 2026-08-04 | sent |
| carbonchain.com | carbonchain.io | CarbonChain | Roheet Shah | roheet@carbonchain.io | 2026-08-04 | sent |
| cogram.com | cogram.com | Cogram | Alexander von Boetticher | alex@cogram.com | 2026-08-04 | sent |
| gocrisscross.com | gocrisscross.com | Crisscross | Richard Lawrence | richard@gocrisscross.com | 2026-08-04 | sent |
| cruitical.com | cruitical.com | Cruitical | Shubham Srivastava | hello@cruitical.com | 2026-08-04 | BOUNCED |
| getdex.com | getdex.com | Dex | Kevin Sun | kevin@getdex.com | 2026-08-04 | sent, SEQUENCE_DONE |
| finta.com | finta.com | Finta | Andy Wang | andy@finta.com | 2026-08-04 | sent |
| gofinto.com | finto.de | Finto | Jonas Morgner | jonasm@finto.de | 2026-08-04 | sent |
| granter.ai | granter.ai | Granter | Bernardo Tavares | bernardo.tavares@granter.ai | 2026-08-04 | sent |
| hyperspell.com | hyperspell.com | Hyperspell | Conor Brennan-Burke | conor@hyperspell.com | 2026-08-04 | sent |
| interfere.com | interfere.com | Interfere | Luke Shiels | luke@interfere.com | 2026-08-04 | sent |
| jinba.io | carnot.ai | Jinba | Shoya Matsumori | contact@carnot.ai | 2026-08-04 | sent |
| leern.io | virtio.io | Leern | Frederik Juulstrup | fj@virtio.io | 2026-08-04 | sent |
| lobuly.com | gmail.com (freemail) | lobuly | Laith Alwanni | alwannicomp@gmail.com | 2026-08-04 | sent |
| mantisbiotech.com | mantisbiotech.com | Mantis | Georgia Witchel | georgia@mantisbiotech.com | 2026-08-04 | sent |
| orangeslice.ai | orangeslice.ai | Orange Slice AI | Vihaar Nandigala | vihaar@orangeslice.ai | 2026-08-04 | sent |
| polyaxon.com | polyaxon.com | Polyaxon | Mourad Mourafiq | mourad@polyaxon.com | 2026-08-04 | sent |
| raycaster.ai | raycaster.ai | Raycaster | Levi Lian | levi@raycaster.ai | 2026-08-04 | sent |
| reflex.dev | reflex.dev | Reflex | Nikhil Rao | nikhil@reflex.dev | 2026-08-04 | sent |
| sapling.ai | sapling.ai | Sapling.ai | Ziang Xie | zxie@sapling.ai | 2026-08-04 | sent |
| signadot.com | signadot.com | Signadot | Arjun Iyer | arjun@signadot.com | 2026-08-04 | sent |
| sustainix.ai | sustainix.ai | Sustainix AI | Dragos Avram | dragos.avram@sustainix.ai | 2026-08-04 | sent |
| systellar-space.com | systellar-space.com | Systellar | Sergi Company Aguilar | sergi.company@systellar-space.com | 2026-08-04 | sent |
| voicepanel.com | voicepanel.com | Voicepanel | John Provine | hello@voicepanel.com | 2026-08-04 | sent |
| gominimal.ai | gominimal.ai | Minimal AI | Niek Hogenboom | niek@gominimal.ai | 2026-08-04 | sent |
| brickwiseai.com | brickwiseai.com | Brickwise | Ismail Jeilani | ismail@brickwiseai.com | 2026-08-04 | sent |
| plexe.ai | plexe.ai | Plexe | Marcello De Bernardi | mdebernardi@plexe.ai | 2026-08-04 | BOUNCED |
| finbar.com | finbar.com | finbar | Edward Huang | ehuang@finbar.com | 2026-08-04 | sent |
| clarm.com | clarm.com | Clarm | Marcus Storm-Mollard | marcus@clarm.com | 2026-08-04 | sent |
| usecrunched.com | usecrunched.com | Crunched | Philip Borge | philip@usecrunched.com | 2026-08-04 | sent |
| bravi.app | bravi.app | Bravi | Anas Bouassami | anas@bravi.app | 2026-08-04 | sent |
| lunavo.ai | lunavo.ai | Lunavo | Felix Loesch | felix.loesch@lunavo.ai | 2026-08-04 | sent |
| dollyglot.com | dollyglot.com | Dollyglot | Paul-Henri Biojout | paul-henri.biojout@dollyglot.com | 2026-08-04 | sent |
| awen.ai | awen.ai | awen | Thibault Henriet | thibault@awen.ai | 2026-08-04 | sent |
| alice.tech | alice.tech | Alice | Kim Rants | kim@alice.tech | 2026-08-04 | sent |
| kyrok.com | kyrok.com | Kyrok | Daniel Hofinger | daniel@kyrok.com | 2026-08-04 | sent |
| oracomputing.com | oracomputing.com | Ora Computing | Stefan Sack | stefan@oracomputing.com | 2026-08-04 | sent |
| skene.ai | skene.ai | Skene | Teemu Kinos | teemu@skene.ai | 2026-08-04 | sent |
| 5u.ai | 5u.ai | 5U | Yagiz Abik | yagiz@5u.ai | 2026-08-04 | sent |
| withclad.com | withclad.com | Clad | Jason Rudin | jason@withclad.com | 2026-08-04 | sent |
| pgdog.dev | pgdog.dev | PgDog | Lev Kokotov | lev@pgdog.dev | 2026-08-04 | sent |
| l2labs.ai | l2labs.ai | L2 Labs | Andrew Bell | andrew@l2labs.ai | 2026-08-04 | sent |
| expanse.org.uk | expanse.org.uk | Expanse | Ismaeel Bashir | ismaeel@expanse.org.uk | 2026-08-04 | sent |
| raindrop.ai | raindrop.ai | Raindrop | Ben Hylak | ben@raindrop.ai | 2026-08-04 | sent |
| pganalyze.com | pganalyze.com | pganalyze | Lukas Fittl | lukas@pganalyze.com | 2026-08-04 | sent |
| hoplite.sh | hoplite.sh | Hoplite | Bence Redmond | bence@hoplite.sh | 2026-08-04 | sent |
| viyamd.com | viyamd.com | ViyaMD | Hari Govardhanam | hari@viyamd.com | 2026-08-04 | sent |
| sourcebot.dev | sourcebot.dev | Sourcebot | Brendan Kellam | brendan@sourcebot.dev | 2026-08-04 | sent |
| traceroot.ai | traceroot.ai | TraceRoot | Xinwei He | xinwei@traceroot.ai | 2026-08-04 | sent |
| magnitude.dev | magnitude.dev | Magnitude | Tom Greenwald | tom@magnitude.dev | 2026-08-04 | sent |
| kernel.sh | onkernel.com | Kernel | Rafael Garcia | raf@onkernel.com | 2026-08-04 | sent |
| dedaluslabs.ai | dedaluslabs.ai | Dedalus Labs | Windsor Nguyen | win@dedaluslabs.ai | 2026-08-04 | sent |
| agenta.ai | agenta.ai | Agenta | Mahmoud Mabrouk | mahmoud@agenta.ai | 2026-08-04 | sent |
| rhesis.ai | rhesis.ai | Rhesis | Harry Cruz | harry@rhesis.ai | 2026-08-04 | sent |
| waleson.com | waleson.com | Waleson | unknown | jouke@waleson.com | 2026-08-04 | sent |
| venedy.io | venedy.io | Venedy | unknown | lukas.huegle@venedy.io | 2026-08-04 | sent |
| silkline.ai | silkline.ai | Silkline | Brent Shulman | brent@silkline.ai | 2026-08-04 | sent |
| rivio.ai | rivio.ai | Rivio | unknown | llarrere@rivio.ai | 2026-08-04 | sent |
| mydatavalue.com | mydatavalue.com | MyDataValue | unknown | martin@mydatavalue.com | 2026-08-04 | sent |
| aqora.io | aqora.io | Aqora | unknown | jannes@aqora.io | 2026-08-04 | sent |
| marpledata.com | marpledata.com | Marple | unknown | nero@marpledata.com | 2026-08-04 | sent |
| skene.ai | skene.ai | Skene | Michele (second contact) | michele@skene.ai | 2026-08-04 | sent |
| unknown | gmail.com (freemail) | unknown | Asbjorn Olling | asbjornolling@gmail.com | 2026-08-04 | sent |
| nozomio.com | nozomio.com | Nozomio | unknown | arlan@nozomio.com | 2026-08-04 | sent |
| leadbay.ai | leadbay.ai | Leadbay | unknown | ludo@leadbay.ai | 2026-08-04 | sent |
| rejot.dev | rejot.dev | ReJot | unknown | founders@rejot.dev | 2026-08-04 | sent |
| zeroentropy.dev | zeroentropy.dev | ZeroEntropy | unknown | founders@zeroentropy.dev | 2026-08-04 | sent |
| helmit.org | helmit.org | Helmit | unknown | info@helmit.org | 2026-08-04 | sent |
| kyrok.com | kyrok.com | Kyrok | unknown (second contact) | info@kyrok.com | 2026-08-04 | sent |
| nomerra.com | nomerra.com | Nomerra | unknown | contact@nomerra.com | 2026-08-04 | sent |
| auxilius.ai | auxilius.ai | Auxilius | unknown | info@auxilius.ai | 2026-08-04 | sent |
| strobepower.com | strobepower.com | Strobe Power | Keeley | keeley@strobepower.com | 2026-08-04 | sent |
| withnixo.com | withnixo.com | Nixo | Priya Khandelwal | priya@withnixo.com | 2026-08-04 | sent |
| kadoa.com | kadoa.com | Kadoa | Adrian Krebs | adrian@kadoa.com | 2026-08-04 | sent |
| goareo.com | goareo.com | AREO | Marius Kirschke | marius@goareo.com | 2026-08-04 | sent |
| archil.com | archil.com | Archil | Hunter Leath | hleath@archil.com | 2026-08-04 | sent |
| minicor.com | minicor.com | Minicor | Faizaan Chishtie | faiz@minicor.com | 2026-08-04 | sent |
| usevawn.com | usevawn.com | VAWN | Alexei Schiopu | alexei@usevawn.com | 2026-08-04 | sent |
| mixpeek.com | mixpeek.com | Mixpeek | Ethan Steininger | ethan@mixpeek.com | 2026-08-04 | sent |
| thoughtmetric.io | thoughtmetric.io | ThoughtMetric | Michael Signorella | mike@thoughtmetric.io | 2026-08-04 | sent |
| funnelstory.ai | funnelstory.ai | FunnelStory | Preetam Jinka | preetam@funnelstory.ai | 2026-08-04 | sent |
| intunedhq.com | intunedhq.com | Intuned | Faisal Ilaiwi | faisal@intunedhq.com | 2026-08-04 | sent |
| guidedclinical.com | guidedclinical.com | Guided Clinical Solutions | Theodore Nguyen-Cao | theo@guidedclinical.com | 2026-08-04 | sent |
| joincarma.com | joincarma.com | Carma | Suleyman Alasgarli | suleyman@joincarma.com | 2026-08-04 | sent |
| halluminate.ai | halluminate.ai | Halluminate | Jerry Wu | jerry@halluminate.ai | 2026-08-04 | sent |
| truthsystems.ai | truthsystems.ai | truthsystems | Nam Nguyen | nam.nguyen@truthsystems.ai | 2026-08-04 | sent |
| imprezia.ai | imprezia.ai | Imprezia | Bishesh Khadka | bishesh@imprezia.ai | 2026-08-04 | sent |
| outship.ai | outship.ai | Outship | Saner Cakir | saner@outship.ai | 2026-08-04 | sent |
| linzumi.com | linzumi.com | Linzumi | Sean Grove | sean@linzumi.com | 2026-08-04 | sent |
| gpt.nexus | gpt.nexus | Nexus | Assem Chammah | assem@gpt.nexus | 2026-08-04 | sent |
| frizzle.com | frizzle.com | Frizzle | Abhay Gupta | abhay@frizzle.com | 2026-08-04 | sent |
| parse.bot | parse.bot | Parse | Alex Forman | alex@parse.bot | 2026-08-04 | sent |
| contextfort.ai | contextfort.ai | ContextFort | Ashwin Ramachandran | ashwin@contextfort.ai | 2026-08-04 | sent |
| dari.dev | dari.dev | dari | Avyay Varadarajan | avyay@dari.dev | 2026-08-04 | sent |
| syntheticsociety.ai | syntheticsociety.ai | Synthetic Society | Aaron Chew | aaron@syntheticsociety.ai | 2026-08-04 | sent |
| useplaygent.com | useplaygent.com | Playgent | Aniruddh Sriram | aniruddh@useplaygent.com | 2026-08-04 | sent |
| sentrial.com | sentrial.com | Sentrial | Neel Sharma | neel@sentrial.com | 2026-08-04 | sent |
| lucenthq.com | lucenthq.com | Lucent | Alisa Rae | alisa@lucenthq.com | 2026-08-04 | sent |
| cyberdesk.io | cyberdesk.io | Cyberdesk | Mahmoud Al-Madi | mahmoud@cyberdesk.io | 2026-08-04 | sent |
| manufact.com | manufact.com | Manufact | Andrew Khadder | andrew@manufact.com | 2026-08-04 | sent |
| openfoundry.ai | openfoundry.ai | OpenFoundry | Tyler Lehman | tyler@openfoundry.ai | 2026-08-05 | sent |
| ncompass.tech | ncompass.tech | nCompass Technologies | Aditya Rajagopal | aditya.rajagopal@ncompass.tech | 2026-08-05 | sent |
| usecrow.ai | usecrow.ai | Crow | Aryan Vij | aryan@usecrow.ai | 2026-08-05 | sent |
| letterbook.ai | letterbook.ai | Letterbook | Dawson Chen | dawson@letterbook.ai | 2026-08-05 | sent |
| okihome.ai | gmail.com (freemail) | Oki | Luofei Chen | chenluofei@gmail.com | 2026-08-05 | sent |
| coldreach.ai | coldreach.ai | Coldreach | Xiaohan Shen | shen@coldreach.ai | 2026-08-05 | sent |
| trystratify.com | trystratify.com | Stratify | Siddhartha Javvaji | sid@trystratify.com | 2026-08-05 | sent |
| oximy.com | oximy.com | Oximy | Naman Ambavi | naman@oximy.com | 2026-08-05 | sent |
| bloomylearning.com | bloomylearning.com | Bloomy | Alex Southmayd | alex@bloomylearning.com | 2026-08-05 | sent |
| getaftercare.com | getaftercare.com | Aftercare | Aidan Lee | aidan@getaftercare.com | 2026-08-05 | sent |
| pothlabs.com | pothlabs.com | Poth Labs | Matthew Wong | matthew@pothlabs.com | 2026-08-05 | sent |
| getdiana.com | getdiana.com | Diana | Upeka Bee | upeka@getdiana.com | 2026-08-05 | sent |
| beglaubigt.de | beglaubigt.de | Beglaubigt.de | Alexander Sporenberg | alexandros@beglaubigt.de | 2026-08-05 | sent |
| castari.com | castari.com | MadeThis (was Castari) | Jacob Wright | jacob@castari.com | 2026-08-05 | sent |
| teachwithscout.com | teachwithscout.com | Scout | Noah Fichter | noah@teachwithscout.com | 2026-08-05 | sent |
| useboom.ai | useboom.ai | Boom AI | Juan Casian | juan@useboom.ai | 2026-08-05 | sent |
| hatchet.run | hatchet.run | Hatchet | Alexander Belanger | alexander@hatchet.run | 2026-08-05 | sent |
| tinfoil.sh | tinfoil.sh | Tinfoil | Tanya Verma | tanya@tinfoil.sh | 2026-08-05 | sent |
| exe.dev | exe.dev | exe.dev | David Crawshaw | david@exe.dev | 2026-08-05 | sent |
| clipper.dev | clipper.dev | Clipper | Kyle Franz | kyle@clipper.dev | 2026-08-05 | sent |
| chonkie.ai | chonkie.ai | Chonkie | Shreyash Nigam | shreyash@chonkie.ai | 2026-08-05 | sent |
| trycua.com | trycua.com | Cua | Francesco Bonacci | f@trycua.com | 2026-08-05 | sent |
| cvector.com | cvector.com | CVector | Joshua Napoli | jnapoli+hn@cvector.com | 2026-08-05 | sent |
| kepler.ai | kepler.ai | Kepler | Eddie Hammond | eddie.hammond@kepler.ai | 2026-08-05 | sent |
| rivergtm.com | rivergtm.com | River | Tarek Abillama | tarek@rivergtm.com | 2026-08-05 | sent |
| bookdna.com | bookdna.com | Book DNA | Ben Fox | ben@bookdna.com | 2026-08-05 | sent |
| alldone.app | alldone.app | Alldone | Karsten Wysk | karsten@alldone.app | 2026-08-05 | sent |
| ploi.cloud | ploi.cloud | Ploi Cloud | Zander van der Meer | zander@ploi.cloud | 2026-08-05 | sent |
| gadabout.ai | gadabout.ai | Gadabout | Yann Eves | yann@gadabout.ai | 2026-08-05 | sent |
| mesmer.co | mesmer.co | Mesmer | Joao de Paula | joao@mesmer.co | 2026-08-06 | sent |
| paraquery.com | paraquery.com | ParaQuery | Win Wang | win@paraquery.com | 2026-08-06 | sent |
| sixtyfour.ai | sixtyfour.ai | Sixtyfour | Saarth Shah | saarth@sixtyfour.ai | 2026-08-06 | sent |
| zarnaai.com | zarnaai.com | Zarna | Rishabh Dhariwal | rishabh@zarnaai.com | 2026-08-06 | sent |
| getsymphony.co | getsymphony.co | Symphony | Shobhit Srivastava | shobhit@getsymphony.co | 2026-08-06 | sent |
| outrove.ai | outrove.ai | Sapien (was Outrove) | Saif Elhager | saif@outrove.ai | 2026-08-06 | sent |
| withriviera.com | withriviera.com | Riviera | Shaun Lane | shaun@withriviera.com | 2026-08-06 | sent |
| motives.ai | motives.ai | Motives | Sean Conley | sean@motives.ai | 2026-08-06 | sent |
| thetokencompany.com | thetokencompany.com | The Token Company | Otso Veistera | otso@thetokencompany.com | 2026-08-06 | sent |
| getcoach.com | getcoach.com | COACH | Mathieu Perez | mathieu@getcoach.com | 2026-08-06 | sent |
| winfunc.com | winfunc.com | Winfunc | Mufeed VH | mufeed@winfunc.com | 2026-08-06 | sent |
| getsolum.com | getsolum.com | Solum Health | JP Montoya | jp@getsolum.com | 2026-08-06 | sent |
| executor.sh | executor.sh | Executor | Rhys Sullivan | rhys@executor.sh | 2026-08-06 | sent |
| sparkles.dev | sparkles.dev | Sparkles | Daniil Bekirov | dan@sparkles.dev | 2026-08-06 | sent |
| superlog.sh | superlog.sh | Superlog | Nicolo Magnante | nicolo@superlog.sh | 2026-08-06 | sent |
| palisade-ai.com | palisade-ai.com | Palisade | Fnu Prince | prince@palisade-ai.com | 2026-08-06 | sent |
| tryalchemize.com | tryalchemize.com | Alchemize | Samuel Fu | sam@tryalchemize.com | 2026-08-06 | sent |
| kausable.ai | kausable.ai | kausable | Benjamin Herdeanu | benjamin@kausable.ai | 2026-08-06 | sent |
| invertix.ai | invertix.ai | Invertix | Kaan Durmaz | kaan@invertix.ai | 2026-08-06 | sent |
| beelzebub.ai | beelzebub.cloud | Beelzebub | Mario Candela | mario.candela@beelzebub.cloud | 2026-08-06 | BOUNCED |
| brainjo.de | brainjo.de | brainjo | Markus Wensauer | m.wensauer@brainjo.de | 2026-08-06 | sent |
| zentio.ai | zentio.ai | Zentio | Christophe Kafrouni | chris.kafrouni@zentio.ai | 2026-08-06 | sent, REPLIED (declined, in-person only) |
| ark-climate.de | ark-climate.de | Ark Climate | Ruth Bosse | ruth@ark-climate.de | 2026-08-06 | sent |
| soren-ai.com | soren-ai.com | Soren | Kevin Xie | kevin@soren-ai.com | 2026-08-06 | sent |
| simplex.sh | simplex.sh | Simplex | Shreya Karpoor | shreya@simplex.sh | 2026-08-06 | sent |
| zerops.io | zerops.io | Zerops | Ales Rechtorik | ales@zerops.io | 2026-08-06 | sent |
| display.dev | gmail.com (freemail) | Display | Ott Ilves | ott.ilves@gmail.com | 2026-08-06 | sent |
| githits.com | githits.com | GitHits | Jaakko (Jack) Timonen | jack@githits.com | 2026-08-06 | sent |
| useautumn.com | useautumn.com | Autumn | Ayush Rodrigues | ayush@useautumn.com | 2026-08-06 | sent |
| strandintelligence.com | strandintelligence.com | Strand Intelligence | Oli Fletcher | oli@strandintelligence.com | 2026-08-06 | sent |
| athenahq.ai | athenahq.ai | AthenaHQ | Andrew Yan | andrew@athenahq.ai | 2026-08-07 | drafted |
| outlit.ai | outlit.ai | Outlit | Josh Earle | josh@outlit.ai | 2026-08-07 | drafted |
| klavis.ai | klavis.ai | Klavis AI | Xiangkai Zeng | xiangkaiz@klavis.ai | 2026-08-07 | drafted |
| spott.io | spott.io | Spott | Lander Degreve | lander@spott.io | 2026-08-07 | drafted |
| dragoneye.ai | dragoneye.ai | Dragoneye | Alex Liao | alex@dragoneye.ai | 2026-08-07 | drafted |
| brightcore.ie | brightcore.ie | BrightCore | Frankie Dolphin | frankie@brightcore.ie | 2026-08-07 | drafted |
| guac-ai.com | guac-ai.com | Guac | Jack Solomon | jack@guac-ai.com | 2026-08-07 | drafted |
| storepass.co | storepass.co | Storepass | Trent Ellingsen | trent@storepass.co | 2026-08-07 | sent, REPLIED (declined) |
| riotiq.com | riotiq.com | Riot IQ | Robert Neir | robertneir@riotiq.com | 2026-08-07 | drafted |
| bucketrobotics.com | bucket.bot | Bucket Robotics | Benjamin Garcia | ben@bucket.bot | 2026-08-07 | drafted |
| fanpad.xyz | fanpad.xyz | FanPad | Sudip Biswas | sudip@fanpad.xyz | 2026-08-07 | drafted |
| mon5.eu | mon5.it | MON5 | Andrea Giovine | andrea.giovine@mon5.it | 2026-08-07 | drafted |
| lytra.ai | lytra.ai | lytra | Etienne Fieg | etienne@lytra.ai | 2026-08-07 | drafted |
| rivulo.ai | rivulo.ai | Rivulo | Mike Miner | mike@rivulo.ai | 2026-08-07 | drafted |
| superglue.ai | superglue.cloud | superglue | Stefan Faistenauer | stefan@superglue.cloud | 2026-08-07 | drafted |
| starsling.dev | starsling.dev | StarSling | Yonas Beshawred | yonas@starsling.dev | 2026-08-07 | drafted |
| tangled.org | tangled.sh | Tangled | Anirudh Oppiliappan | anirudh@tangled.sh | 2026-08-07 | drafted |
| endform.dev | gmail.com (freemail) | Endform | Jakob Norlin | jakob.stahl91@gmail.com | 2026-08-07 | drafted |
| sequa.ai | gmail.com (freemail) | Sequa AI | Fabian Emilius | fabian.emilius@gmail.com | 2026-08-07 | drafted |
| proliferate.com | pablohansen.com | Proliferate | Pablo Hansen | pablo@pablohansen.com | 2026-08-07 | drafted |
| openworklabs.com | prologe.io | OpenWork | Ben Shafii | ben@prologe.io | 2026-08-07 | drafted |
| cactuscompute.com | gmail.com (freemail) | Cactus Compute | Henry Ndubuaku | ndubuakuhenry@gmail.com | 2026-08-07 | drafted |
| unsloth.ai | gmail.com (freemail) | Unsloth AI | Daniel Han | danielhanchen@gmail.com | 2026-08-07 | drafted |
| expectedparrot.com | gmail.com (freemail) | Expected Parrot | John Horton | john.joseph.horton@gmail.com | 2026-08-07 | drafted |
| stagewise.io | outlook.com (freemail) | stagewise | Glenn Toews | glenntoews@outlook.com | 2026-08-07 | drafted |
| omnara.com | gmail.com (freemail) | Omnara | Kartik Sarangmath | kartiksarangmath@gmail.com | 2026-08-07 | drafted |
| runanywhere.ai | runanywhere.ai | RunAnywhere | Sanchit Monga | san@runanywhere.ai | 2026-08-14 | drafted |
| gooseworks.ai | athina.ai | Gooseworks | Himanshu | see-gmail-draft-2026-08-17 | 2026-08-17 | drafted |
| upliftai.org | upliftai.org | Uplift AI | Zaid Qureshi | see-gmail-draft-2026-08-17 | 2026-08-17 | drafted |

## RECOVERED FROM THE LOST 17 AUGUST RUN — read this before the next run

The 17 August Task 1 run made four changes to this file and **could not push them**. The container
was discarded, so they were reconstructed here by hand on 18 August from the run report and the
Gmail drafts. Three of the four are done. **One is still outstanding.**

**Applied:**

- `hello@hugentic.ai` (Mark Bird) moved to `sent, REPLIED`. He replied at 13:04 UTC on 14 August
  and this campaign never follows up a thread with a real human reply in it.
- Five rows moved to `sent, FOLLOWED_1_DRAFTED` — **Airweave, Ambral, Artificial Societies,
  assistant-ui, Balance**. These are the 2 August cohort the run drafted follow-ups to at 08:13 on
  17 August. The drafts exist in Gmail and may or may not have been sent yet, which is exactly what
  that status means.

**Also applied, 18 August — the two new companies are now in the table:**

Gooseworks — company domain `gooseworks.ai`, email domain `athina.ai`, person Himanshu, dated
2026-08-17, status `drafted`. Uplift AI — both domains `upliftai.org`, person Zaid Qureshi, same
date and status.

(Deliberately written as prose rather than as a table, so that a parser scanning for pipe-delimited
rows cannot mistake this description for two extra records.)

**These rows block correctly as they stand.** Blocking is by `company_domain` OR `email_domain` OR
exact email, so `gooseworks.ai`, `athina.ai` and `upliftai.org` all land in `BLOCKED_DOMAINS` and
neither company can be sourced again. The email cell is a placeholder and that costs nothing,
because the domain match fires first.

**Two notes so nobody "fixes" these rows wrongly:**

- **Gooseworks' email domain is not its website domain.** The address the 17 August run verified
  sits on `athina.ai` while the company being pitched is `gooseworks.ai`. Both belong in the row
  and both get blocked. That is what the two-domain column layout is for.
- **Tidy-up, whenever convenient and not urgent:** open the two 08:27 drafts from 17 August in
  Gmail, read the `To:` addresses, and replace `see-gmail-draft-2026-08-17` with the real values.
  Nothing depends on it — the blocking already works — but the record should say what was actually
  sent.
- Uplift AI appears in the "From 14 August" rejected section below as a near miss, dropped then for
  publishing only `founders@upliftai.org`. The 17 August run found a personal address for Zaid
  Qureshi. **That near-miss note is out of date; the row above supersedes it.**

## Still worth reconciling before the next run

A 13 August audit found the 7 August rows reading `drafted` while Gmail showed them in Sent. There
are **25** such rows in the table today (the twenty-sixth, Storepass, has since moved to
`sent, REPLIED (declined)`).

Separately, **14 rows read `sent, FOLLOWED_1_DRAFTED`** — Hey Telo, Hugentic (now REPLIED),
Indexable, Inkbox, Limrun, Meticulate, Moss, nao Labs, o11 and Onlook, plus the five added above.
That status means a follow-up draft exists but may never have been sent. Check Gmail and move each
to `sent, FOLLOWED_1` if it went, or leave it if it did not.

Neither drift changes who is blocked — every one of those statuses blocks — but both make the
follow-up eligibility set wrong.

## Verified but NOT contacted — safe to use, do not block

- **Phrasing**, Benjamin Barrell, `hn@phrasing.app`, 1 person, Netherlands. Dropped on 5 August
  only because `hn@` is a role-style alias and the exact publication could not be re-confirmed.
  It is a solo founder, so the alias does reach him.

(stagewise, Omnara and Cactus were on this list and were used on 7 August. Their rows are in the
table above.)

## Rejected with a reason worth keeping

Not blocked, but do not waste calls re-researching these without new information.

**From 6 August**

- **Quin AI** (iamquin.ai) — no named human founder verifiable anywhere, generic company mailbox,
  and the product's own terms call it an experimental research demo rather than a product.
- **Aedilic / GPUDeploy** (gpudeploy.com) — inactive on its YC page, both founders listed as
  former, domain parked and for sale.
- **LetSorted** (letsorted.co.uk) — the only published address for the founder sits on
  rendmate.com, a separate agency, not the startup.
- **FanShares** (fansharesapp.com) — two self-described non-technical founders, no specific HQ.
- **Record OS, Mimir, Emdash, Canary, Oddpool** — real companies that pass the filters, but the
  only published address for each is a shared inbox. Held back because **five of five bounces to
  date have been shared inboxes.**
- **Tentris** (tentris.io) — the only published address for the named co-founder is his university
  address, not a company address.

**From 7 August**

- **Homie** (usehomie.com), Markku Vuorinen, Helsinki, 5. A Cision release prints
  `markku@usehomie.co` while the same release gives the website as `usehomie.com`. The one-letter
  difference could not be resolved from a second source. **Worth one manual check** if Faisal
  wants it.
- **Beacon** (getbeacon.cloud), London. The launch release signs off "Julian Kahn, Founder &
  Director, julian@getbeacon.cloud" while the body of the same release quotes "Chris Williams,
  Founder & Director". Internally inconsistent, so dropped.
- **The Robot Learning Company** (robot-learning.co), 1 person, Germany. Verified personal address
  and passes headcount and HQ, but the product is sub-$10k robot arms with imitation-learning
  control. Too far from web, mobile and cloud work. **Reinstate if robotics comes into scope.**
- **Anori Tech** (anoritech.com), 3, Hamburg. Verified personal address, but the product is
  `no_std` Rust battery-management firmware. Same reasoning.
- **The Context Company, Humwork, Menza, Ara** — all 2 to 3 people, all pass the filters, but each
  publishes only a `founders@` address and it appears on their YC launch post rather than their
  own site.
- **Ossprey** (7, London), **ARC Intelligence** (8, Berlin), **Tower Computing** (12, Berlin),
  **ThatRound** (9), **Hyground** (11), **Stilla** (12), **Exhibitly** (3) — stated headcount, real
  products, shared inboxes only.
- **MiM / Aesir Technology**, **Ounas Health**, **Docupath** — personal address verified, but no
  source states team size, so they fail the never-estimate rule. **Closest to salvageable if a size
  can be found.**

**From 13 August** (0 new drafts — every candidate failed a hard filter)

- **FlexDesk** (flexdesk.com), NYC, 8. Clark Jacobs, CEO, `clark@flexdesk.com` genuinely published
  on the YC launch post. Dropped **only** because the YC jobs listing says "Remote (US)".
  **Reinstate if a source ever shows them accepting remote outside the US.**
- **Nectar** (nectarclimate.com), SF, 7. Allen Wang, `allen@nectarclimate.com`, published on his
  own site. Same problem.
- **Flex** (withflex.com), SF, 8. Sam O'Keefe, `sam@withflex.com`, published in podcast show notes.
  Same problem.
- **Infrawatch** (infrawatch.com), London, 5 distributed — good remote evidence, but every address
  was broker-masked or `users.noreply.github.com`.
- **Emphere** (emphere.com), Seattle, 5 — no remote evidence, no personal email.
- **cubic** (cubic.dev), 3–6, London — the company's own YC jobs page lists only an on-site London
  role. Also deep in the AI-coding-tool niche this campaign is already saturated in.
- **~140 others** screened across YC, HN "Who is hiring" (August 2026), Wellfound, WeWorkRemotely,
  RemoteOK and funding-news searches, rejected almost entirely for two reasons: **only a shared
  inbox was ever published**, or **no page anywhere states an exact headcount** (third-party
  crawler estimates do not count).

**From 14 August** (1 new draft, from ~185 companies across three research passes)

- **Educato** (educato.com), SF, 5. Good remote evidence. Dropped only because no personal email
  exists for either founder — `founders@` plus banned `support@`/`press@`/`info@`.
  **NEAR MISS — shared inbox only.**
- **Uplift AI** (upliftai.org), SF, 3. Voice AI for Urdu and Bengali. Good remote evidence. Only
  `founders@upliftai.org` published. RocketReach-style guesses were found and **correctly not
  used** — those are pattern guesses, not published evidence. **NEAR MISS.**
- **Ref** (hirewithref.com), 5 stated in their own Greenhouse posting, genuinely worldwide remote.
  Dropped because **no founder or decision-maker name could be verified anywhere.**
- **Icon** (icon.com), NY. Found a genuine personal email, `kennan@icon.com`, on the company's own
  /story and /careers pages. Dropped because the only open engineering role is explicitly "Hybrid"
  and no core-team headcount is stated (200+ editors and 1,288+ creators are gig contractors, not
  the core team).
- **RunAnywhere** passed and is in the table. **Its address required care and the lesson
  generalises:** the YC page displayed link text `san@runanywhere.ai` and a first WebFetch
  confirmed it cleanly. A second pass asking for the raw mailto href **contradicted itself** —
  quoted `san@` then speculatively claimed the target "uses sanchit@ based on context". Per the
  unreadable-response rule that entire second response was discarded. **`sanchit@runanywhere.ai`
  was never used**, because it only ever appeared as a model's inference, which is exactly the
  pattern-completion this campaign must never act on.
- **~175 others** screened (YC launches, YC remote-jobs board, HN "Who is hiring" August and July
  2026, Greenhouse/Lever/Ashby/Workable API slug sweeps, remote newsletters, npm/PyPI maintainer
  records, recent funding news) and rejected for: remote restricted to US-only / hybrid / a
  timezone band excluding UTC+5; headcount too large or never stated by a real source; shared
  inbox only; or no personal email findable at all.

## Sourcing notes worth keeping

- **The "Remote (US)" trap**, found 13 August. Most YC jobs-page listings that say "Remote"
  actually say **"Remote (US)"** once you open the page, which fails the filter as hard as
  "hybrid" does. On 13 August this alone killed three fully-verified companies with genuine
  personal emails. **Screen for the exact word after "Remote" before doing any email verification
  work**, not after.
- **Press-release contact lines are the single highest-yield source for personal addresses.** The
  "Media contact: [Founder Name], [email]" pattern produced every personal address in the
  funding-news lane on 7 August, whereas /contact and /impressum pages produced almost nothing but
  `info@`.
- **Public git commit author headers remain the best source for open-source founders.** Fetch
  `https://api.github.com/repos/OWNER/REPO/commits` and read the author email, or open a commit as
  a `.patch` URL. Skip anything ending `users.noreply.github.com`. **Ten of the twenty-six on
  7 August came from this.**
- **Exa renders Cloudflare-obfuscated addresses as the literal string `[email protected]`**, which
  silently hides real addresses on several German sites. Only recoverable from a non-obfuscated
  source.
- **Found 14 August:** asking WebFetch to inspect a raw mailto href separately from the visible
  link text can produce a self-contradicting answer. Treat that as UNREADABLE and fall back to
  whatever the page's plain visible text showed consistently across independent fetches. **Never
  adopt the speculative "corrected" address.**
- **Found 14 August:** YC company pages remain strong (headcount, remote evidence and sometimes a
  real mailto in one page), but three passes across ~185 companies surfaced only **1** fully
  verified personal email against 4 that failed solely on shared-inbox or missing decision-maker.
  That matches the ~6 percent guidance. **A thin day here is a correct outcome, not a tooling
  failure.**
