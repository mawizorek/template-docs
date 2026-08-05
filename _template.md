---
# REQUIRED.
# No status, no page. # set once, NEVER change it
# No id, no links.
# No summary, no search result.
id: kebab-case-forever          
title: What A Human Reads
status: hidden | unlisted | public
type: page | index | venue | space | standard | procedure | reference
summary: One or two lines on what this is and who needs it.

# ---- Uncomment what this page needs ----

# REQUIRED BY TYPE. Delete unless the type above needs it.
# parent: building-id           # `space` only

# OPTIONAL. Any of these, in any combination, or none.
# order: 10                     # plain integer, unquoted. absent = alphabetical
# revised: 2026-08
# theme: eos
# related: [some-id, another-id]
# xref: [peer-site:their-page-id]
# source: https://where-the-facts-came-from
# keywords: [genie, personnel lift, MEWP, LX]

# CONDITIONAL - data tables. The slot NAME must be legal for the type above.
# data:
#   schedule:                   # reference: schedule survey inventory_table
#     file: circuit-schedule.tsv#            revision_log catalog
#     caption: Circuit schedule # optional

# CONDITIONAL - routers. All four are one feature.
# router: [staff, pm]           # engine tables. LIST, never a repeated key
# router_code: [tryme]          # written here, so public. throwaway only
# router_prompt: Got a code?    # DEAD unless one of the two above is present
# router_inherit: false         # only if a parent folder declares a router

# CONDITIONAL - index lists. Opposite ends of one relationship.
# contents: auto                # THIS page lists its children (non-index types)
# indexed: false                # keep THIS page out of its parent's list

# CONDITIONAL - the sidebar. THIS FILE'S NAME MUST BE index.md OR IT DOES
# NOTHING. The repo's ROOT index.md sets the default all the others inherit.
# nav: expand | collapse | hide
---

<!-- Copy this file, rename it kebab-case, drop it in the right folder.
     That registers it: there is no index to update and no nav file to edit.

     Then, in this order:
       1. Set id, title and summary. Set status when it is ready to be seen.
       2. Uncomment only the header lines this page needs.
       3. Delete every line you did not use -- including this comment.
       4. Replace the H1 and the sections below.

     ⚠️ DO NOT WRITE A PARAGRAPH UNDER THE H1. That used to be the lede and it
     is now `summary:` above. A paragraph there renders as ordinary body text
     under the real lede, usually saying the same thing twice, and the build
     reports it.

     ⚠️ IF A VALUE IS NOT NEEDED AWAY FROM THIS PAGE, IT IS NOT A HEADER KEY.
     Write it in the body, or put it in a TSV. A dozen fields were removed on
     2026-08-03 for failing that test.

     ⚠️ `also_known_as` WAS RENAMED TO `keywords` (2026-08-04). The old key is
     valid YAML, so it parses, gets ignored, and silently does nothing. The
     build names every page still using it.

     ⚠️ `nav:` IS NEW (2026-08-05) AND IS index.md ONLY. On any other page it
     is ignored and reported. It decides what a FOLDER does in the sidebar --
     and the root index.md decides it for every folder that stays quiet.

     A page that ships carrying `Section heading`, `Revised Month Year`, or a
     stray commented-out key is the first thing an audit finds.

     WHAT EACH KEY MEANS, AND THE AUDIT CHECKLIST:
     Authoring -> The gold standard. The keys are listed above; the rules
     behind them are not restated here. -->

# New page

## Section heading

Plain paragraph. Blank line between every block.

## Related

- [Using these docs](@using-these-docs)
