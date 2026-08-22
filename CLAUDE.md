# guestgraph/.github — working conventions

This repository holds the organisation profile shown on github.com/guestgraph:
`profile/README.md`. That is its entire contents.

## The one rule that matters

**A second repository links, never restates.**

This profile once said "Core in development" while two slices had shipped, because it
restated a roadmap that lives in the engine repository. Nothing detected it — no CI in
one repository can validate prose in another, and the profile is the page a first-time
visitor reads before anything else.

So the profile carries positioning and links, and nothing that has an owner elsewhere:

| Fact | Owner — link to it |
|---|---|
| What the product does, concepts | the engine repo's `README.md` |
| Matching behaviour, thresholds | the engine repo's `docs/matching.md` |
| Roadmap, deferred work, status | the engine repo's `docs/roadmap-notes.md` |
| API surface | the engine repo's `specs/*/contracts/openapi.yaml` |
| The talk | `guestgraph/talks` |
| The pitch | guestgraph.io |

Before adding a sentence here, ask what would have to change if the answer changed. If
the answer is "a file in another repository", link to it instead.

## Editing

`profile/README.md` renders on the org page. There is no build and no preview — GitHub
renders it directly, so check it on github.com/guestgraph after pushing.

Keep it short. It competes with the repository list directly beneath it.

## Process

- Commits happen when Rob asks; suggest a message, don't auto-commit.
- Never mention closed-source predecessor projects — here, in docs, or in commits.
