---
id: template
title: gold-template
type: page
status: public
order: 99
revised: 2026-08
---

# The gold standard TEMPLATE

<!---
---
# REQUIRED. No status, no page. No id, no links.
id: kebab-case-forever          # set once, NEVER change it
title: What A Human Reads
status: hidden                  # hidden -> unlisted -> public
type: page                      # page index venue space standard procedure reference

# REQUIRED BY TYPE. Delete unless the type above needs it.
parent: building-id             # `space` only

# OPTIONAL. Any of these, in any combination, or none.
order: 10                       # plain integer, unquoted. absent = alphabetical
revised: 2026-08
theme: eos
related: [some-id, another-id]
source: https://where-the-facts-came-from

# CONDITIONAL - routers. All four are one feature; see the guide.
router: [staff, pm]             # engine tables. LIST, never a repeated key
router_code: [tryme]            # written here, so public. throwaway only
router_prompt: Got a code?      # DEAD unless one of the two above is present
router_inherit: false           # only if a parent folder declares a router

# CONDITIONAL - index lists. Opposite ends of one relationship.
contents: auto                  # THIS page lists its children (non-index types)
indexed: false                  # keep THIS page out of its parent's list
---
--->

# Page Title

One or two lines. This is the lede: it renders large, and it is also what the
search result shows.

Two things that are always true and cause most of the trouble:

- **Blank line between every block.** Paragraphs, lists, headings, tables.
- **Callout bodies indent four spaces.** See [Writing a page](@writing).

!!! danger "`status: gated` is not a gate"
    It is **not implemented**. A page declaring it is published as `unlisted`
    with a warning in the build log: a live URL, absent from the sidebar, and
    not protected in any way. A `gate:` key beside it does nothing at all.

  
