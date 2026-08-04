---
id: example-house
title: Example House
type: venue
status: public
order: 0
summary: A building that does not exist, documented as though it does, so the renderer can be checked against something with no consequences.
revised: 2026-08
---

# Example House

1 Placeholder Street, Somewhere. Operated by Nobody In Particular.

## Spaces

- [Main Stage](@main-stage) -- the fully documented case
- [Studio](@studio) -- deliberately incomplete, to show what a marked gap looks like

## Why a fake venue

Because the gold standard has to be safe to break. Every real site in this
family has readers who would be misled by a half-finished example page. This
one has none, so it can carry a page with missing facts on purpose and a link
that points nowhere on purpose.

## What changed here

The address line above was frontmatter until 2026-08-03, drawn as a generated
table by the `venue` type. It is a sentence now. An address is a fact about a
building, printed on that building's page and read by nothing else, which is
the test that removed it. See [Frontmatter](@frontmatter).
