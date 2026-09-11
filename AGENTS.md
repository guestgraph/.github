<!-- conventions · v1.10.0 -->
Shared conventions of the robertblust, guestgraph and companygraph organizations live in
`conventions/`, vendored from robertblust/conventions at the release `conventions.json`
names. Read them before writing or committing anything here.

- `conventions/WRITING.md` — how we write: one voice, three registers, English and German.
- `conventions/WORKING.md` — how we work with git and GitHub.
- `conventions/REPOSITORIES.md` — the family: what each repository is and what pins what.
- `conventions/WRITER.md`, `conventions/TRANSLATOR.md`, `conventions/GLOSSARY.md` — the two roles that
  make a text, and the terms they keep.

Everything below this block is this repository's own. `sh conventions/conventions-sync check`
says whether the copy matches the release, `sync` brings it to the release the pin names, and
`sh conventions/conventions-check` holds this repository's own Markdown to `WRITING.md`. Edit
a shared file in robertblust/conventions, never here.
<!-- end conventions -->

# guestgraph/.github — working conventions

This repository holds the organization profile shown on github.com/guestgraph:
`profile/README.md`. That is its entire contents.

## The one rule that matters

**A second repository links, never restates.**

This profile once said "Core in development" while two slices had shipped, because it
restated a roadmap that lives in the engine repository. Nothing detected it — no CI in
one repository can validate prose in another, and the profile is the page a first-time
visitor reads before anything else.

The lesson is about restating, not about owning. Two facts a first-time visitor needs before
they open any repository are owned here and linked from the engine: which phases have shipped,
and which services run and what they talk to. Everything else has an owner elsewhere and is
linked, never repeated:

| Fact | Owner |
|---|---|
| Which phases shipped, which come next | **here**, `profile/README.md` — the engine's README links to it |
| Which services run, what they expose and hold | **here**, `profile/README.md` — the component diagram |
| What the product does, concepts | the engine repo's `README.md` |
| Matching, profiles, identifiers, records, timeline, continuity | the engine repo's `docs/` — one document each |
| Requirements captured for later slices | the engine repo's `docs/roadmap-notes.md` |
| API surface | the engine repo's `specs/*/contracts/openapi.yaml` |
| The talk | `guestgraph.github.io`, at `talks/` — served at guestgraph.io/talks/ |
| The pitch | guestgraph.io |

**What is owned here is owned here alone.** A phase list or a component diagram copied into a
repository README is the same drift in the other direction, and just as invisible.

Before adding a sentence here, ask what would have to change if the answer changed. If
the answer is "a file in another repository", link to it instead.

## Editing

`profile/README.md` renders on the org page. There is no build and no preview — GitHub
renders it directly, so check it on github.com/guestgraph after pushing.

Keep it short. It competes with the repository list directly beneath it.

## Checks

One job, required by the ruleset on `main`: `conventions`, called from robertblust/conventions
at the pinned tag and shown by GitHub as `conventions / conventions`. There is nothing else to
check: the profile has no build and no suite. Everything about how to write and how to work
with git is in `conventions/`; this file is only what is this repository's own.
