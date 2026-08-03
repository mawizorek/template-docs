---
id: links
title: Links
type: page
status: public
order: 20
revised: 2026-08
---

# Links

Internal links name a page's `id`, never its file path. That single decision is
why reorganising this repository cannot break it.

## Within this site

```markdown
[Main Stage](@main-stage)
[the venue notes](@main-stage#venue-notes)
```

Moving the file, renaming its folder or retitling the page cannot break either
of those, because none of those things is what the link points at.

A heading you link to needs an explicit anchor:

```markdown
## Venue notes {#venue-notes}
```

Without it the link is riding on the heading TEXT, which dies the moment
somebody rewords it. Working example: [the studio's access
notes](@studio#access).

## To a sibling site

```markdown
[the rep plot](@oph:rep-plot)
```

The part before the colon names a peer site, configured in the engine. Every
site in the family publishes a `/doc-index.json` listing its page ids, and that
is what a cross-site link resolves against.

**The honest limit:** this resolves at BUILD time, not when a reader clicks. If
a sibling renames a page, links to it stay wrong until the next build. A
nightly rebuild closes that to about a day. Closing it further would mean
running a server, which is a bad trade for a documentation archive.

## When a link does not resolve

It renders struck through with a `[broken link]` marker and lands in the build
report. It does **not** fail the build.

That is a deliberate reversal of how the first version worked. Building in
strict mode meant one typo froze the entire live site -- twice in forty minutes
on one occasion -- while Pages cheerfully kept serving a stale commit and gave
no indication anything was wrong. One ugly link on one page is a far better
outcome than a site that silently stops updating.

Here is what one looks like: [a page that does not
exist](@no-such-page-anywhere).

## Never use a full URL for an internal page

A hardcoded `https://` link to another page in this family will not be checked,
will not be reported when it breaks, and will not survive the site moving. Use
the id.
