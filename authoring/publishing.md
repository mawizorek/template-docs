---
id: publishing
title: Publishing
type: page
status: public
order: 40
revised: 2026-08
---

# Publishing

How a page you have written becomes a page a reader can see. It is one
deliberate action, and it is not the same thing as saving the file.

## The link

**[Publish a site](https://github.com/mawizorek/doc-render-engine/actions/workflows/publish.yml)**

Run workflow → pick the site → pick `preview` or `publish`.

## Saving is not publishing

Committing a file to a content repo does **nothing** to the live site. That is
not an oversight to work around; it is the shape of the system.

A content repo holds markdown and nothing else, including no build workflow of
its own, which is what keeps its Download ZIP clean and makes the whole tree
portable. The cost is that a content repo cannot rebuild itself. The benefit is
the one that matters day to day: **an unfinished page can sit in `main` for a
week without a reader ever seeing it.** Going live is a decision somebody
makes, not a side effect of hitting save.

So `status: public` in frontmatter means *this page is allowed to be
published*. The publish run is what actually publishes it. Two gates, and both
have to be open.

## Always preview first

`preview` renders the site, compares it against what is **actually being served
right now**, and deploys nothing. The run summary tells you:

- 🆕 **New pages**, with the URL each will land on
- 🗑️ **Pages that will disappear**, which is the one to read carefully
- ✏️ **Renamed, moved or re-typed pages**, old value → new value

Then run it again with `publish` if the diff is what you expected.

!!! warning "Read the disappearing list every time"

    A page vanishes for two very different reasons -- it was deleted, or its
    `status:` is no longer public -- and they look identical in this report.

    It also matters beyond this site: if another site links to that page's
    `id`, its next build renders a broken reference. Ids are a promise, and
    removing one quietly breaks somebody else's page.

## What the preview cannot tell you

It compares the **page index**: ids, titles, URLs, types. It does not compare
prose.

Rewrite every paragraph on a page and the preview reports no change, correctly.
It is answering *what pages exist and where do they live*, not *what do they
say*. Do not read a quiet report as "nothing changed."

## Confirming it landed

Look at the **footer stamp** on the live page. It names the run that built what
you are looking at.

This is the only reliable signal, because a failed build is invisible: GitHub
Pages keeps serving the last version that worked, with no banner and no error.
The site just stops changing. If the stamp does not name your run, the deploy
did not take -- check the workflow run rather than refreshing.

Allow about a minute after a green publish.

## Related

- [Publication states](@publication) -- what `hidden`, `unlisted` and `public`
  mean, and the honest limits of each
- [Frontmatter](@frontmatter) -- where `status:` lives
