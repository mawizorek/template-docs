---
id: using-these-docs
title: Using these docs
type: page
status: public
order: 1
revised: 2026-08
summary: How to read a site in this family, and what the small visual signals on a page actually mean.
---

# Using these docs

## The footer stamp is the honest signal

Every page footer carries a PR number or a commit hash. That is not decoration.

When a build fails, GitHub Pages does not show an error. It keeps serving the
last version that worked, with no banner and no warning. The site simply stops
changing. If you pushed an edit and the footer stamp is not your change, **the
build failed** -- the page you are reading is stale, and nothing on the site is
going to update until it is fixed.

## The first line under a title is the summary

It renders larger and lighter than the body, and it is also the text you see
under a page's name in a search result. If a search result has a title and no
text beneath it, that page has not been given one.

## Marked values tell you how much to trust them

Facts on these pages are written in the prose, not in a generated table, and
where a value is uncertain it says so **inside the sentence**:

- **To be confirmed** -- written down, not checked against a source
- **Verify on site** -- recorded once, never re-checked. Measure before you
  build to it
- **Not recorded** -- this fact should exist and does not. The absence is
  known, not overlooked
- **Confirmed** -- checked against the real thing
- **~Estimate** -- close enough to plan with, not to cut to
- ~~Superseded~~ -- the old value, kept so older paperwork still matches up

Hover any of them on the live site for the same explanation.

**"Not recorded" is the one worth understanding.** A missing fact and a fact
that does not exist look identical, and a reader will draw the wrong conclusion
and never know they did. A room with no recorded grid height reads exactly like
a room with no grid. Marking the gap is what makes it fixable.

!!! note "This section used to describe a generated table"

    Until 2026-08-03, venue and space pages carried a grey field table drawn
    automatically from the page's header, plus a *"Not documented yet"* box
    naming anything left blank. Both were removed: the facts they held belong
    in the document, not in its metadata. If you remember those and cannot find
    them, that is why.

## Struck-through links are broken

A link rendered with a line through it and a `[broken link]` marker pointed at
a page that does not exist, or at a sibling site that could not be reached. It
is marked instead of hidden on purpose: a dead link that looks alive is worse
than a missing one, because you trust it and find out later.

A link with a small arrow leads to a **different site** in the family.

## Editing

Every page has an *Edit this page on GitHub* link at the foot. It opens the
source markdown. Phone is fine. Commit, wait a minute or two, then check the
footer stamp.
