# previews/

Task 3 commits its generated HTML preview pages here, one folder per run date:

```
previews/2026-08-18/carving-rock-kitchen.html
previews/2026-08-18/goodman-coffee-roasters.html
```

One self-contained file per lead, **both categories**. Call leads get one too, so Faisal can send
it the moment somebody asks to see something.

## Rules for the HTML

- **Everything inline.** Inline CSS, no external stylesheets, no frameworks, no CDN links, no
  JavaScript beyond what is genuinely needed. **It must render offline.**
- Real business name, real services, real city, taken from the audit. **Never invent a service
  they do not offer.**
- Show the three problems found and what fixed looks like. Honestly and specifically.
- Mobile-first. The pitch is usually that their current site is not.
- Tasteful and restrained. This is a work sample, so it is also an audition.
- Footer line: `Concept prepared by Faisal Hanif - faisalhanif.work`

## Hosting is manual, and that is why the link check exists

The run generates the file. **Faisal uploads it** to `https://faisalhanif.work/p/<slug>`.

The email carries the link **only if the run fetched that exact URL and got HTTP 200.** No 200,
no link — the sentence changes to an offer to send the concept instead.

So on any morning the pages have not been uploaded yet, every email ships link-free. That is
correct behaviour. The packet lists which slugs need uploading, and Faisal can upload them and
decide for himself whether to paste a link back in before pressing Send.

The reason this is a fetch and not a warning: on 14 August four real businesses received emails
pointing at pages that had been generated but never uploaded. Every link 404'd. The risk had been
written down in advance and guarded with a capitalised note. That is not enough.
