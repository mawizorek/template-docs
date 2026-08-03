---
id: onboarding-a-site
title: Onboarding a new site
type: procedure
status: public
order: 30
owner: Whoever owns the engine repo
frequency: Whenever a new documentation site is needed
trigger: A new subject area that deserves its own audience and its own URL
systems: Engine repo, content repo, GitHub Pages
revised: 2026-08
---

# Onboarding a new site

How a new documentation site joins this family. Included here for a structural
reason as much as a practical one: it is a page with no venue, no space and no
theatre anywhere in it.

That matters. A doc engine built only against theatre content quietly grows
theatre-shaped assumptions, and nobody notices until the first site that is
not a theatre tries to use it. A procedures-only page has to be a first-class
citizen here or the portability claim is decoration.

## The procedure

1. **Create the content repo.** Markdown only. Nothing else, ever.
2. **Add an instance** in the engine: copy the template instance folder, edit
   its config for the new site's name, URL, content repo and palette.
3. **Add one row** to the build matrix in the engine's workflow.
4. **Enable Pages** on the new content repo, deploying from the `gh-pages`
   branch. The first build creates that branch; the setting is flipped once
   afterwards.

## Two rules that come with joining

**Do not share a palette.** The sites should not look identical. The day
somebody edits a shared colour to fix one site is the day another breaks in a
way nobody notices for a month. Structure is shared; look is local.

**Pin the engine by tag, never by branch.** The entire reason these are
separate repositories is that they fail separately. A floating reference
re-couples them, and one bad engine commit takes down every site at once. Run
the lowest-stakes site as the canary on the moving tag and pin the rest behind
it.
