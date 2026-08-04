---
description: Add one deep-analysis card to analysis/index.html from a pasted article (for sources that require login, e.g. Fugle blog, StatementDog industry reports)
---

The user will provide a source URL and the full text of an article they copied themselves (they had to log in to read it — you never have access to gated content directly). Their input follows this command as `$ARGUMENTS`. If `$ARGUMENTS` is empty, ask them to paste the URL and article text.

Do this:

1. Read `analysis/index.html` in the current repo to see the live design and existing cards — match its exact markup/CSS conventions, don't invent new ones.
2. From the pasted text, figure out:
   - **Source pill text**: infer a short site/publication name from the URL's domain (e.g. `blog.fugle.tw` → "富果直送", `statementdog.com` → "財報狗產業報告"). If the domain is unfamiliar, use the site's own name if visible in the pasted text, otherwise ask.
   - **Date**: use the article's own published date if present in the pasted text (MM/DD format, matching other cards); otherwise today's date.
   - **Headline**: the article's real title, Traditional Chinese, lightly tightened if needed for card-heading length — never invent a different claim than the source makes.
   - **Summary** (the visible `<p>`): 2-3 sentences, your own paraphrase of the article's core argument and any concrete numbers/names it gives. Never copy sentences verbatim or use quotation marks around source text — this is a hard copyright rule, same as the rest of this site.
   - **Tags**: 3-5 short tags (tickers/companies/industries/topics mentioned).
   - **`.card-detail`**: two more paraphrased paragraphs going deeper into specifics from the pasted text (not just restating the summary).
   - **`data-url`**: the exact article URL the user gave you.
3. Insert a new `<article class="card">` block into `analysis/index.html`'s `.cards` container, following the exact structure of the existing cards there (`card-meta` with `src-pill` + `card-time`, `<h3>`, summary `<p>`, `.tags`, hidden `.card-detail` with the two extra `<p>`s, then `.card-link`). Add it, don't replace any existing card, unless the user's URL matches one already on the page (then update that one in place instead of duplicating).
4. If the trailing note paragraph below `.cards` (the one listing which sources had content this week) is stale relative to what's now on the page, update it to include the newly added source.
5. Confirm the file is well-formed (balanced tags), then:
   ```
   git add analysis/index.html
   git -c user.name="Andy Wu" -c user.email="wuandy258@gmail.com" commit -m "Add [source name] card to deep analysis page"
   git push origin main
   ```
6. Report back concisely: which card was added, its headline, and confirm it's pushed.

Only ever base the summary and detail paragraphs on what the user actually pasted — if their pasted text is thin, write a shorter but still honest card rather than filling gaps with invented specifics.
