---
id: home
title: Doc Family Template
type: index
status: public
order: 0
revised: 2026-08
---

# Doc Family Template

The working reference for how every site in this family is written, rendered
and published. Every page here is both an explanation and a live example of the
thing it explains.

## Start here

If you are about to write a page, read [Using these docs](@using-these-docs)
and then [Frontmatter](@frontmatter). Between them they take about five minutes
and cover everything that is genuinely mandatory.

If you are standing up a new site, the engine's own README is the procedure.
This site is the thing you copy.

## What is demonstrated here

| Section | What it proves |
| --- | --- |
| [Authoring](@authoring) | The frontmatter contract, links, publication states |
| [Venues](@venues) | The `venue` and `space` types, parent chains, generated spec tables |
| [Standards](@standards) | The `standard` and `procedure` types, including a page with no theatre in it |
| [Reference](@reference) | The `reference` type |

## The rule everything else follows from

This repository contains markdown and nothing else. No stylesheet, no config,
no nav file, no build machinery. Everything that turns these documents into a
website lives in a separate engine repository.

The reason is the green **Download ZIP** button. A content repo that is purely
content can be handed to somebody, archived, printed, or imported somewhere
else without anyone having to explain which folders to ignore.
