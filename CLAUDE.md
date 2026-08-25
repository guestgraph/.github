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
| The talk | `guestgraph.github.io`, at `talks/` — served at guestgraph.io/talks/ |
| The pitch | guestgraph.io |

Before adding a sentence here, ask what would have to change if the answer changed. If
the answer is "a file in another repository", link to it instead.

## Editing

`profile/README.md` renders on the org page. There is no build and no preview — GitHub
renders it directly, so check it on github.com/guestgraph after pushing.

Keep it short. It competes with the repository list directly beneath it.

## Process

- Commits happen when the user asks; suggest a message, don't auto-commit.
- **Merge a pull request with a merge commit — `gh pr merge --merge`, never `--squash`.**
  Squashing is not a history preference here. GitHub *re-authors* a squash commit to the
  account that pressed the button, so a commit made locally under the wrong `user.email`
  lands on the default branch looking correct. That is not hypothetical: it was found in
  `robertblust.github.io`, where the local commit was authored `rob@likemagic.tech` and the
  commit that reached `main` read `robert.blust@flatland.ch`, with nothing anywhere saying
  so. A merge commit preserves the author it was given, which is the point — a wrong
  identity surfaces instead of being laundered.
- **The author is `robert.blust@flatland.ch`, and nothing on GitHub enforces it.** The
  ruleset rule that would — `commit_author_email_pattern`, a metadata restriction — is
  rejected on this plan. Tested, not assumed: an otherwise identical ruleset carrying a
  `deletion` rule was accepted in the same breath. So the identity comes from
  `~/.gitconfig`, where three `includeIf` blocks key it to `~/git/robertblust/`,
  `~/git/guestgraph/` and `~/git/companygraph/` and point at `~/.gitconfig-flatland`. The
  global default stays `rob@likemagic.tech`, which is right for `~/git/likemagic-tech` and
  `~/git/3ap-ag`. A clone made outside those three directories gets the global default and
  no warning, so check `git config user.email` before the first commit in a fresh clone.
- Never mention closed-source predecessor projects — here, in docs, or in commits.
