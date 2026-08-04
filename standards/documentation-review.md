---
id: documentation-review
title: Documentation review
type: standard
status: public
order: 10
summary: What has to be true of a page before it is allowed to be public, and how often somebody checks that it still is.
revised: 2026-08
---

# Documentation review

**Decided by the site owner. Applies to every page on every site in this
family. Reviewed annually, and whenever the engine changes behaviour.**

Those three facts are the first thing on the page on purpose. A standard that
does not say who decided it, and when somebody next checks it, is folklore:
nobody can point to the decision and nobody notices when it stops being true.

## Before promoting a page to public

1. Every required field for its type is filled in: `id`, `title`, `status`,
   `summary`, plus `parent` on a space.
2. `summary` says what the page is and who needs it, in one or two lines. It is
   what a search result shows, so a page without one is findable and
   unreadable.
3. No leftover paragraph under the H1 saying the same thing as `summary`.
4. The H1 matches `title`. Nothing reconciles them for you.
5. Every link resolves. Check the build report, not your memory.
6. `revised` reflects when the content was last true, not when the file was
   last touched.

## What review is not

It is not a spelling pass. It is a check that the facts on the page are still
facts. A beautifully written page describing a room that was rebuilt two years
ago is worse than no page, because somebody will act on it.

## Related

- [The gold standard](@audit), the full checklist this summarises
- [Rigging inspection](@rigging-inspection), a procedure beside this standard
