---
id: example-house
title: Example House
type: venue
status: public
order: 0
address: 1 Placeholder Street
city: Somewhere
operator: Nobody In Particular
revised: 2026-08
---

# Example House

A building that does not exist, documented as though it does, so that the
renderer can be checked against something with no consequences.

Everything above the fold on this page is generated. The address, city and
operator rows are drawn by the `venue` type from frontmatter, not typed into
the body. Compare with the spaces below, which get a different set of fields
from the `space` type without anybody deciding that per page.

## Spaces

- [Main Stage](@main-stage) -- the fully documented case
- [Studio](@studio) -- deliberately incomplete, to show what a gap looks like

## Why a fake venue

Because the gold standard has to be safe to break. Every real site in this
family has readers who would be misled by a half-finished example page. This
one has none, so it can carry a page with missing fields on purpose and a link
that points nowhere on purpose.
