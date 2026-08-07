---
id: data-tables
title: Data tables
type: page
status: public
order: 7
revised: 2026-08
summary: How a TSV beside a page becomes a table on it, what a header cell can declare, why a half-filled row turns into a heading, and how to switch the phone layout off.
---

# Data tables

A `.tsv` sitting beside a page can be drawn as a table on it. The file stays a
spreadsheet on disk, so it is editable in Excel or Numbers, diffable in git, and
the reader gets a download link to the exact file the table was drawn from.

This page is the canonical description of that feature. If something else in
this family disagrees with it, this page is right and the other one has rotted.

!!! warning "If you are rewriting a TSV, read The header line first"

    The first line of a data file can carry declarations that look like part of
    the column name. They are a handful of characters and easy to type over.
    That has already happened twice, and both times the page silently lost a
    feature nobody noticed until somebody opened it on a phone.

## Putting a table on a page

Two halves. The frontmatter names a **slot**, and the body places it.

```yaml
data:
  catalog:
    file: course-index.tsv
    caption: Optional
```

```
!!! data "catalog"
    pin: thtr
    sort: thtr
    hide: slug, family
```

**The body never names a file, only a slot.** That is what lets the same
paragraph be copied between Audio, LX and Video with only the frontmatter
changed.

A slot is always a map with a `file:` key. `caption:` is optional. There is no
second legal form, and the old list-of-filenames shape is ignored and reported.

### Options

All four are optional, and all four are indented under the block.

| Option | What it does |
| --- | --- |
| `pin` | freezes a column against the left edge while the rest scrolls |
| `sort` | orders rows within each section |
| `hide` | drops a column from the VIEW, comma separated |
| `caption` | overrides the frontmatter caption |

An option naming a column that does not exist is **reported in the build and
ignored**. It never fails the build and it never fails silently.

⚠️ `hide` removes a column from the PAGE, not from the file. The download still
has it. That is the intended way to keep an identifier available without
printing it on the page.

### Linking to one

```markdown
[the circuit schedule](@data:circuit_schedule)
```

The name is the slot, never the filename. If the table is embedded on the page
the link jumps to it; if the slot is declared and never placed, the link
downloads the file. See [Links](@links).

## The header line can declare each column

```
thtr::id.key    slug    title::.key    credits::num    unit_cost::money
```

The shape is `name::type.role`, and both halves are optional. `x::num` is a type
with no role, `x::.key` is a role with no type, and a plain `x` is neither.

**A plain column name is completely fine.** The renderer reads the values and
works out what a column holds. You only annotate the columns it gets wrong.

### Types

| Type | Use it for | What changes |
| --- | --- | --- |
| `id` | an identifier that happens to be digits | mono, left, tabular figures |
| `num` | a quantity | mono, right, tabular figures |
| `money` | an amount | `num`, plus a currency symbol and two decimals |
| `date` | an ISO timestamp | printed as `Aug 4 · 7:58p` |
| `text` | a short label or code | mono, one line |
| `prose` | a sentence | wraps, body font |

**Three cases the renderer gets wrong on its own**, which is the entire reason
the grammar exists:

- A course number is **entirely digits**, so it reads as a quantity and
  right-aligns as though you might add the codes up. It is a name that happens
  to be written in digits. Hence `::id`.
- A credits column holding `1-4` alongside `3` and `4` has **one non-numeric
  value**, which drops the whole column to text and the figures stop lining up.
  Hence `::num`.
- An ISO stamp is **a string to any heuristic** and a moment in time to a
  reader. Hence `::date`.

Currency is the same class and worse: `1200` is a number either way, and nothing
in the values says dollars.

⚠️ **`money` and `date` store the RAW value and change only what is printed.** A
money column holds a plain number and the site draws the symbol; a date column
holds the full ISO stamp and the site prints a short form. Both still sort
correctly and both still open correctly in a spreadsheet.

⚠️ **A `date` has no format option, deliberately.** One site, one date format.
The short form drops the year, which suits a log of recent activity and would
not suit one spanning years. If that comes up it argues for a second type, not
a per-column pattern.

⚠️ An unknown type or role is reported in the build and ignored, so a typo like
`::pros` costs you the styling and tells you why rather than failing quietly.

## A row with one filled cell becomes a heading

This is the rule that surprises people, and until now it was written down
nowhere.

**If the first cell of a row is filled and every other cell in that row is
empty, the row is drawn as a section heading** spanning the whole table, not as
a record.

```
ID      NAME              COUNT
RACK 1
INV-70  SM58              6
INV-71  Beta 58A          2
RACK 2
INV-88  Spirit Folio      1
```

`RACK 1` and `RACK 2` become bands. That is the feature working: a real exported
sheet is full of headings like `WIRED MICROPHONES [8170]`, and drawing them as
mostly-empty records is how a sheet gets misread.

!!! warning "There is no way for a row to say it is a record"

    The rule is positional and has no override. **A genuine record you have not
    finished filling in will render as a heading**, and deleting the last value
    from a sparse row silently converts it into one. Nothing is reported,
    because from the outside a half-filled row and a section band are the same
    shape.

**The fix is one character in any other cell.** A single `-` is enough to make
the row a record again, and it is the house convention for a value that does not
exist yet.

```
INV-92  -                 -
```

⚠️ **The column still has to be titled.** An untitled column whose every cell is
`-` is dropped from the table entirely, which puts the row straight back to
being a heading. A titled column full of dashes keeps its header and stays, so
in practice this only bites on trailing columns nobody named.

So you do **not** have to fill every row with real data. You have to keep every
row from being empty past its first cell.

## Roles, and the phone layout

A column marked `.key` stays visible when the page runs out of room.

On a **narrow** container, a table with any `.key` column stops being a table.
Each row becomes one line of the key columns, and everything else appears
labelled when the row is tapped. The last key column is the title; anything
before it is a small line above it.

```
THTR 123
Intro to Lighting for the Stage        v
-----------------------------------------
CREDITS   4
LAB       section
ENGL      124
```

### Marking a column `.key` is the whole switch

There is nothing else to turn on, and **nothing else to turn off.** A file that
marks no key keeps the ordinary sideways-scrolling table everywhere, on every
screen size.

!!! good "Turning the collapsing rows off again"

    Delete `.key` from every header cell in that TSV. That is the entire
    revert. No frontmatter change, no option, no engine change, and the file is
    a plain scrolling table again the next time the site builds.

⚠️ If every visible column is a key, there is nothing to reveal, so no chevron
appears and the rows are simply a list. That is the intended shape, not a
missing control.

### When it fires

The list layout is driven by the width of the **table's own container**, not by
the width of the window and not by what device you are on. The renderer never
learns what device it is on and cannot: the site is built once and the same
bytes are served to everybody.

!!! warning "Desktop showing a list is a browser difference, not your sheet"

    Container queries are not resolved identically by every browser engine. The
    same page, at the same window size, can fold into list mode in one browser
    and render a full table in another. If you see collapsing rows on a full
    desktop window, **check it in a second browser before changing the file** --
    this has already cost one round of fixes to a sheet that was correct.

## Who owns the header line

**Whoever writes the header declares the spec.** This is the rule that decides
where an annotation goes, and getting it wrong means the annotation disappears
on a schedule nobody is watching.

| Header written by | So the spec lives |
| --- | --- |
| a person | in the file |
| an export from FileMaker or similar | in the exported field name |
| a workflow, on a schedule | in the workflow script |

Anything typed by hand into the header of an **exported** sheet survives until
the next export and then vanishes, with no error and nothing to read. A sheet
regenerated by a workflow is worse, because it can regenerate every few minutes.
Both are fixed the same way: **change the thing that writes the header, not the
file it wrote.**

### The same trap has a human version

A hand-maintained sheet is safe from machines and **not safe from us.** One
course index has been overwritten twice by sessions doing unrelated work: first
a column rename, then a pass adding links to 43 titles, each of which rewrote
the whole file and typed the header from memory.

Neither was careless. Both wrote a header that looked exactly like a header. Git
raised no conflict, because one side wrote a line the other side had never seen
change.

!!! note "If you rewrite a data file"

    Re-read it immediately before you write, and keep the header line you find
    rather than the one you remember. That is the only check there is. Nothing
    validates this, and the failure is invisible on a desktop.

## What the renderer will not do

Filters, totals, renamed columns, computed columns. Those edit the data, and the
sheet is the source of truth: the renderer draws it, it does not reinterpret it.

`hide` is allowed because dropping a column from a view does not change what the
sheet says. `money` and `date` are allowed because they change how a value is
printed rather than what it is. Those are the only exceptions and they are meant
to stay the only ones.

A cell can contain anything a sentence can: confidence markers, `@` references,
bold, code. Sorting works on the plain text underneath, so **marking a value
cannot reorder the sheet.**

⚠️ A marked cell stops being a number to **Excel**, which is why confidence
belongs on prose rather than on figures you intend to add up. See
[Markers](@markers).

## One trap in the frontmatter above the table

Not a data-table rule, but it has broken four pages in one night and this is
where somebody will look.

```yaml
title: THTR 131 Design for the Stage: Scenery      # breaks the page
title: "THTR 131 Design for the Stage: Scenery"    # correct
```

An unquoted YAML value containing a colon-and-space is read as a nested key, so
the frontmatter fails to parse, so **the page never builds and every link to it
renders as a dead reference.** The page does not appear broken; it appears
absent.

**Quote any title, summary or caption containing a colon followed by a space.**

## Related

- [Writing a page](@writing) -- hand-written tables, and when one wants to
  become a data file instead
- [Links](@links) -- `@data:` mentions, and every other reference form
- [Frontmatter](@frontmatter) -- the block at the top, and what may go in it
- [Markers](@markers) -- confidence on a single value, inside a cell or a
  sentence
