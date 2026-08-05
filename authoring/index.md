---
id: authoring
title: Authoring
type: index
status: public
order: 0
revised: 2026-08
summary: Everything you need to write a page and get it published.
---

# Authoring

## The ninety-second version

Drop a `.md` file in the right folder. Give it frontmatter. That is the whole
registration process -- there is no index to update and no nav file to edit,
because neither of those things is allowed to exist in a content repo.

```markdown
---
id: rehearsal-studio
title: Rehearsal Studio
type: space
status: hidden
summary: The second-floor rehearsal room, and what it can and cannot hold.
parent: example-house
---

# Rehearsal Studio

## What is in it
```

Note what is **not** there: no paragraph under the H1. That used to be the
lede and it is now `summary:`. Note also that nothing in the header describes
the room -- no capacity, no dimensions. Those go in the body.

Start every new page at `status: hidden`. Promote it when it is worth reading.

Then [publish](@publishing) -- saving the file does not put it on the site.

## The rules that actually matter

1. **Every page needs `status` and `summary`.** No status, no build -- that is
   deliberate, so nothing reaches the public web because somebody forgot a
   line. No summary, and the page appears in search with nothing under its
   name.
2. **Never change an `id`.** Other pages link to that string, including pages
   on other sites. Changing it breaks them silently.
3. **Link to ids, never to file paths.** See [Links](@links).
4. **Facts about the subject go in the body**, never in the header. There is no
   field for a capacity or an address, and that is on purpose.

## Start here

- [The gold standard](@audit) -- the whole frontmatter block in one copyable
  piece, ordered required to conditional, plus the audit checklist and the list
  of keys that look real and do nothing

## Writing

- [How this works](@how-this-works) -- where documents, machinery and config
  each live, and the two questions that decide where a new thing goes
- [Frontmatter](@frontmatter) -- every field, what it does, which are required,
  and the rule that decides whether a new one may exist at all
- [Writing a page](@writing) -- callouts, department tabs, tables, and the
  four-space indent rule that causes most formatting trouble
- [Callout gallery](@callouts) -- every callout family rendered on one page, so
  you can pick one by looking instead of guessing from its name
- [Links](@links) -- `@id`, headings, and cross-site references
- [Markers](@markers) -- `{.tbc}`, `{.conf}`, `{.gap}` and friends: saying how
  much a value can be trusted, and getting a list of every one on the site

## Publishing

- [Publication states](@publication) -- hidden, unlisted, gated, public, and the
  honest limits of each
- [Publishing](@publishing) -- the publish workflow, the preview diff, and how
  to confirm a deploy actually landed
- [Routers](@routers) -- a text field that sends someone to a page if they know
  the code. Soft, not a lock.
