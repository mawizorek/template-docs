---
# REQUIRED. No status, no page. No id, no links.
id: kebab-case-forever          # set once, NEVER change it
title: What A Human Reads
status: hidden                  # hidden -> unlisted -> public
type: page                      # page index venue space standard procedure reference

# ---- Everything below is commented. Uncomment what this page needs,
# ---- DELETE every line you do not use, then delete these four rules.

# REQUIRED BY TYPE. Delete unless the type above needs it.
# parent: building-id           # `space` only

# OPTIONAL. Any of these, in any combination, or none.
# order: 10                     # plain integer, unquoted. absent = alphabetical
# revised: 2026-08
# theme: eos
# related: [some-id, another-id]
# source: https://where-the-facts-came-from

# CONDITIONAL - routers. All four are one feature.
# router: [staff, pm]           # engine tables. LIST, never a repeated key
# router_code: [tryme]          # written here, so public. throwaway only
# router_prompt: Got a code?    # DEAD unless one of the two above is present
# router_inherit: false         # only if a parent folder declares a router

# CONDITIONAL - index lists. Opposite ends of one relationship.
# contents: auto                # THIS page lists its children (non-index types)
# indexed: false                # keep THIS page out of its parent's list
---

<!-- Copy this file, rename it kebab-case, drop it in the right folder.
     That registers it: there is no index to update and no nav file to edit.

     Then, in this order:
       1. Set id and title. Set status when the page is ready to be seen.
       2. Uncomment only the header lines this page needs.
       3. Delete every line you did not use -- including this comment.
       4. Replace the H1, the lede, and the sections below.

     A page that ships carrying `Section heading`, `Revised Month Year`, or a
     stray commented-out key is the first thing an audit finds.

     WHAT EACH KEY MEANS, AND THE NINE-QUESTION AUDIT CHECKLIST:
     Authoring -> The gold standard. The keys are listed above; the rules
     behind them are not restated here. -->

# New page

One sentence on what this is and who needs it. This renders as large lede text
by itself, and it is also what the search result shows. Keep it to one or two
lines and do not try to make it big yourself.

## Section heading

Plain paragraph. Blank line between every block.

## Related

- [Using these docs](@using-these-docs)
