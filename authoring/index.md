---
id: authoring
title: Authoring
type: index
status: public
order: 0
revised: 2026-08
---

# Authoring

Everything you need to write a page and get it published.

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
parent: example-house
---

# Rehearsal Studio

One sentence on what this is and who needs it.
```

Start every new page at `status: hidden`. Promote it when it is worth reading.

Then [publish](@publishing) -- saving the file does not put it on the site.

## The three rules that actually matter

1. **Every page needs `status`.** No status, no build. That is deliberate:
   nothing reaches the public web because somebody forgot a line.
2. **Never change an `id`.** Other pages link to that string, including pages
   on other sites. Changing it breaks them silently.
3. **Link to ids, never to file paths.** See [Links](@links).

## Writing

- [Frontmatter](@frontmatter) -- every field, what it does, which are required
- [Writing a page](@writing) -- callouts, department tabs, tables, and the
  four-space indent rule that causes most formatting trouble
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
