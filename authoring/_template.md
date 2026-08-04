---
id: template
title: The gold standard TEMPLATE
type: page
status: public
order: 99
revised: 2026-08
summary: The block, ready to copy, with every real key in the order the spec puts them.
---

# The gold standard TEMPLATE

```yaml
---
# REQUIRED. No status, no page. No id, no links. No summary, no search result.
id: kebab-case-forever          # set once, NEVER change it
title: What A Human Reads
status: hidden                  # hidden -> unlisted -> public
type: page                      # page index venue space standard procedure reference
summary: One or two lines. THE LEDE. Not a paragraph under the H1 any more

# REQUIRED BY TYPE. Delete unless the type above needs it.
parent: building-id             # `space` only

# OPTIONAL. Any of these, in any combination, or none.
order: 10                       # plain integer, unquoted, NO leading zero
revised: 2026-08
theme: eos
related: [some-id, another-id]
source: https://where-the-facts-came-from
also_known_as: [genie, personnel lift, MEWP]   # renders visibly at the foot

# CONDITIONAL - routers. All four are one feature; see the guide.
router: [staff, pm]             # engine tables. LIST, never a repeated key
router_code: [tryme]            # written here, so public. throwaway only
router_prompt: Got a code?      # DEAD unless one of the two above is present
router_inherit: false           # only if a parent folder declares a router

# CONDITIONAL - index lists. Opposite ends of one relationship.
contents: auto                  # THIS page lists its children (non-index types)
indexed: false                  # keep THIS page out of its parent's list
---

# Page Title

## First real section
```

Two things that are always true and cause most of the trouble:

- **Blank line between every block.** Paragraphs, lists, headings, tables.
- **Callout bodies indent four spaces.** See [Writing a page](@writing).

!!! danger "`status: gated` is not a gate"

    It is **not implemented**. A page declaring it is published as `unlisted`
    with a warning in the build log: a live URL, absent from the sidebar, and
    not protected in any way. A `gate:` key beside it does nothing at all.

## Related

- [The gold standard](@audit)
- [Frontmatter](@frontmatter)
