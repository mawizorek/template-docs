---
id: using-these-docs
title: Using these docs
type: page
status: public
order: 1
revised: 2026-08
---

# Using these docs

How to read a site in this family, and what the small visual signals on a page
actually mean.

## The footer stamp is the honest signal

Every page footer carries a PR number or a commit hash. That is not decoration.

When a build fails, GitHub Pages does not show an error. It keeps serving the
last version that worked, with no banner and no warning. The site simply stops
changing. If you pushed an edit and the footer stamp is not your change, **the
build failed** -- the page you are reading is stale, and nothing on the site is
going to update until it is fixed.

## Spec tables are generated, not typed

The grey field table near the top of a venue or space page is drawn by the
page's declared **type**, not written by the author. Every space in the family
gets the same fields in the same order.

This is why they can be trusted to be comparable, and why a field that is
missing on one page is genuinely missing rather than just formatted
differently.

## "Not documented yet" means exactly that

When a page shows a *Not documented yet* note naming some fields, it is saying
those facts have not been recorded. It is **not** saying the thing does not
exist.

A space with no grid height used to look identical to a space with no grid.
Saying it out loud turns a silent gap into a visible one, which is the only way
a gap ever gets filled.

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
