# template-docs

The gold-standard content repo. **Pure markdown, and that is the point.**

**Live site:** https://mawizorek.github.io/template-docs/
**Rendered by:** https://github.com/mawizorek/doc-render-engine

---

## Why this repo has nothing in it but documents

Click the green **Code → Download ZIP** button. What you get is the documents
and nothing else. No stylesheet to delete, no config to explain, no build
folder to ignore, no template file that is not really a page.

That is the requirement this whole family was designed around, and it is the
reason the renderer lives in a different repository entirely. Everything that
turns these files into a website -- hooks, themes, object schema, site config,
the deploy workflow -- is over in the engine. This repo is documents. The
engine knows about this repo; this repo does not know about the engine.

**The rule, in full: this tree holds markdown and nothing else. Ever.** No nav
file, no template, no stylesheet, no script, no config. A `.md` file, its
frontmatter block, and where a page genuinely needs one, an image beside it.

If something seems like it needs to live near the content, the answer is that
it belongs in the engine and the hook that reaches for it is the missing piece.

## The built site is on another branch, and that is deliberate

The rendered HTML is pushed to `gh-pages` by the engine. It never touches
`main`, because the green button zips the DEFAULT branch only -- so the
download stays pure while the site still lives at a normal URL.

Do not commit to `gh-pages` by hand. It is overwritten by every build.

## Why this particular repo exists

This is the **executable specification** for every doc site in the family.

A written gold standard rots. Somebody changes the engine, nobody updates the
prose, and six months later the document describes a system that no longer
exists. An executable one cannot do that: if the template renders correctly,
the spec is true by demonstration. If a change breaks the contract, this site
breaks first and loudest, before any site with actual readers.

So it does two jobs at once. It **documents** the authoring contract, and by
building successfully it **proves** the contract. Every page in here is also a
worked example of the thing it describes.

Copy from this repo when starting a new site. Keep it ordinary: no clever
exceptions, no special cases, nothing another site could not imitate. A copy
inherits the habits of its source.

## Working in here

- Branch, commit, PR, self-merge. Never direct to `main`.
- Every page needs `id`, `title`, and `status`. A page with no `status` does
  not build, which is how nothing goes public by accident.
- Never change a page's `id`. Other pages link to that string.
- Do not add a non-markdown file. That is the one rule with no exceptions.
- **Editing here does not trigger a rebuild.** This repo holds no workflow, by
  design. The engine rebuilds on a nightly schedule, or immediately if someone
  runs its workflow by hand. That latency is the price of purity and it is paid
  on purpose.

## The one thing to be honest about

This repo is public and so is the site. A GitHub Pages site is publicly
reachable **even when its repository is private** -- privately published Pages
needs GitHub Enterprise Cloud. Publication states control what reaches the
site, never what is readable in the repo.

So the test before writing anything, in any repo in this family: if a stranger
read this page, would it matter? If yes, it does not belong in a doc repo.
