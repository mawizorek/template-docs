---
id: new-page
title: New page
type: page
status: hidden
---

<!-- ─────────────────────────────────────────────────────────
     NEW PAGE TEMPLATE

     1. Copy this file. Rename it kebab-case: rehearsal-studio.md
     2. Drop it in the right folder. That registers it. There is no
        index to update and no nav file to edit, because neither is
        allowed to exist in this repo.
     3. Set id, title and type. Leave status: hidden until it is worth
        reading.
     4. Delete every block you do not use, including this comment.

     ID      The permanent name other pages link to. Usually the filename
             without .md. SET IT ONCE AND NEVER CHANGE IT: that promise is
             what makes links survive a move.

     TYPE    page | venue | space | standard | procedure | reference
             The type decides which fields are required and what gets
             drawn automatically. See Authoring -> Frontmatter.

     STATUS  hidden    not built at all, URL 404s        (start here)
             unlisted  live URL, no sidebar, no search
             gated     NOT IMPLEMENTED -- behaves as unlisted
             public    listed, searchable, done
     ───────────────────────────────────────────────────────── -->

# New page

One sentence on what this is and who needs it. This first paragraph renders as
large light lede text automatically, and it is also what the search result
shows. Do not try to make it big yourself, and keep it to one or two lines.

## Section heading

Plain paragraph. Blank line between every block: paragraphs, lists, headings,
tables. That single rule prevents most formatting surprises.

<!-- CALLOUTS. The body MUST be indented four spaces. That is the whole trick.

     !!! note "Title"      context, gaps, placeholders
     !!! warning "Title"   costs money or wastes a day
     !!! danger "Title"    a genuine safety stop
-->

## Related

<!-- INTERNAL LINKS ARE IDS, NEVER PATHS:
       a page     [Main Stage](@main-stage)
       a heading  [the notes](@main-stage#venue-notes)
       a sibling  [rep plot](@oph:rep-plot)
     A heading you link to needs an explicit {#anchor}. -->

- [Using these docs](@using-these-docs)
