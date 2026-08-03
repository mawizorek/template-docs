---
id: authoring
title: Authoring
type: page
status: public
order: 0
revised: 2026-08
---

# Authoring

Everything you need to write a page correctly, in three short documents.

## The ninety-second version

Drop a `.md` file in the right folder. Give it frontmatter. That is the whole
registration process -- there is no index to update and no nav file to edit,
because neither of those things is allowed to exist in this repo.

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

## The three rules that actually matter

1. **Every page needs `status`.** No status, no build. That is deliberate:
   nothing reaches the public web because somebody forgot a line.
2. **Never change an `id`.** Other pages link to that string. Changing it
   breaks them silently.
3. **Link to ids, never to file paths.** See [Links](@links).

## The three documents

- [Frontmatter](@frontmatter) -- every field, what it does, which are required
- [Links](@links) -- `@id`, headings, and cross-site references
- [Publication](@publication) -- hidden, unlisted, gated, public, and the
  honest limits of each
