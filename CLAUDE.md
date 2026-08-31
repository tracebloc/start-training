# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this repo does

Jupyter notebook quick-start guide for running ML training experiments on the tracebloc platform. Walks users through connecting their account, uploading a model, linking a dataset, configuring training parameters, and starting an experiment.

## Notebook locations

- `notebooks/traceblocTrainingGuide.ipynb` -- main training guide. Open it in
  Colab straight from this repo:
  [colab.research.google.com/github/tracebloc/start-training/…](https://colab.research.google.com/github/tracebloc/start-training/blob/main/notebooks/traceblocTrainingGuide.ipynb)
  (tracks `main`, so a merged fix reaches users on the next promotion).

  > There is also a Drive-hosted copy,
  > [`drive/1N00idt…`](https://colab.research.google.com/drive/1N00idtpoaq1lk9OJE6g4bMqd8o-Qex2C?usp=sharing),
  > which the web app's "Start training" button still points at. It is **not**
  > version-controlled: nothing in this repo can change it, so a fix landed
  > here does not reach that copy. Either the button is repointed at the
  > GitHub-backed URL above (tracebloc/frontend-app), or someone with Drive
  > access re-uploads this notebook on every change. Until one of those
  > happens, assume the Drive copy is stale (backend#2862).
- `notebooks/GenerateCheckWeights.ipynb` -- utility for generating/checking model weights

## How users run it

### Google Colab (recommended)
Open the Colab link, copy to Drive, and run cells.

### Locally
```bash
pip install "tracebloc[pytorch]>=0.14.0"
jupyter notebook notebooks/traceblocTrainingGuide.ipynb
```

On **Python 3.11-3.14** (the SDK's `requires-python`). An out-of-range
interpreter fails as `No matching distribution found for tracebloc`, which
looks like a missing package and is not one -- the notebook's preflight cell
exists to say which it is (backend#2862).

## Prerequisites

- Python 3.11-3.14
- A tracebloc account
- An active use case with a dataset
- A model file (from the [model-zoo](https://github.com/tracebloc/model-zoo) repo or custom)

## Key dependency

[`tracebloc`](https://pypi.org/project/tracebloc/) (PyPI, 0.8.x+) -- the Python SDK used in the notebook to authenticate, upload models, and start training.

> Was published as `tracebloc_package` before 0.8.0. The old install command (`pip install tracebloc_package`) still resolves via a metadata-only redirect on PyPI, but new notebooks should use the canonical `tracebloc` name.

<!-- org-standards:begin -->
## tracebloc engineering standards (org-wide)

<!-- Canonical source: tracebloc/.github/org-standards.md.
     Synced into every repo's CLAUDE.md between org-standards markers — never
     edit it inside a consuming repo; open a PR against tracebloc/.github.
     Meta-rule: the moment a rule below becomes mechanically enforced (a lint
     rule, a house-rules grep, a required check), delete the sentence here and
     let the check carry it. Prose is only for what tooling can't judge. -->

### Branches & PRs

- Branch model, **for a repo on the release train**: `develop → staging → main`. Branch off `develop`; every PR targets `develop`. Never open PRs to `staging` or `main` — promotions are the train's job.
- **For a repo not on the train, do not infer the branch model from this file — read `repo-inventory.yml`.** `release_train:` says whether the model above applies at all, and the per-branch `exempt:` anchors record which branches actually exist. This bullet used to enumerate the exceptions by name and **drifted from the inventory on every one of them**: `docs` was called `main`-only while it had been on the train since 2026-08-04 (`release_train: true`, `develop: required`, staging present), and `rfcs` was called `main`-only while it had a `develop` taking merges (measured 2026-08-22, backend#2242 / .github#306). Restating the authority is the defect; pointing at it is the fix.
- **Trap, recorded in the inventory and caught by no check:** a `develop` created on a non-train repo and left **unprotected** is invisible to the guards — that is the `develop_unprotected_non_train` anchor, and the inventory notes "a `develop` created and left UNPROTECTED is not flagged … no check was going to surface it." So creating one to satisfy the first bullet **forks the repo silently**: PRs split between the new branch and the repo's existing convention, nothing promotes between them, and the two heads diverge until someone reconciles by hand. If a repo appears to lack a `develop`, that is a fact to verify in the inventory, not a gap to fill.
- Before starting any task: `git fetch` and branch from the current tip of `develop` — never build on a stale checkout. A branch that lives more than a day gets `develop` merged back in before review. We move fast; stale starts mean silent divergence and duplicated work.
- One self-contained change per PR. A few hundred changed lines reviews well; at 1000+ split it. Refactors ship in separate PRs from behavior changes.
- Branches are short-lived (aim to merge within a day or two), single-author, and based on `develop` — no stacked PRs on top of other open PRs.
- Your branches are yours to clean up. Merged ones now delete themselves server-side, so this is about the rest: run `git reap` (from `tracebloc/.github/scripts/git-reap`) in your checkouts now and then. It is dry-run by default and only proposes a branch when it can prove the work landed. Nobody else can do this for you — you are the only one who knows whether an *unmerged* branch of yours still matters, and `git branch --merged` will not tell you, because we squash-merge and a squashed branch is not an ancestor of `develop`.
- **"Yours" is the branch you opened the PR for, never the branch whose last commit is yours.** Pushing a review fixup onto someone else's branch makes you its tip-commit author and changes nothing about whose work it is — so a "my branches" list built from `%(authorname)`, or from the tip author in any form, aims your cleanup at other people's work. Measured: two of Shujaat's `client` branches showed up on such a list and were one confirmation step away from `--delete` (backend#2365). If you are building any list that reasons about ownership, call `tracebloc/.github/scripts/branch_owner.py` rather than re-deriving it; a branch it cannot attribute comes back as `unattributable`, which is the answer to act on, not to fill in.
- Names and commits: `feat/ fix/ docs/ sec/ ci/ chore/` + issue number + short slug (`fix/1234-ingest-timeout`); commit subjects `type(scope): summary`, referencing the ticket (`backend#1234`).
- When you open a PR: assign yourself and request exactly one reviewer immediately — a PR without a reviewer stalls by construction. You pick the reviewer: whoever knows the code best. There is no per-repo default, and no automation assigns one — branch protection just refuses to merge without a review.
- When you are the reviewer: first response within one business day.

### Quality bar

- Before every push: run the linter and the tests that cover your change. Never push a branch you believe is red — CI is the backstop, not the first run.
- Read the full diff before opening the PR. You own every line you ship, whoever — or whatever — wrote it.
- AI sessions end with evidence, not assertion: run the relevant check (tests, build, lint) and show the output. A change that could not be verified does not ship.
- Fix the class, not the instance. The bug you just fixed is a member of a class; check the rest of the class before you push. Two shapes, and aiming at only the first catches half of them: **other call sites** — grep the symbol or pattern you changed — and **other inputs to the same guard** — what else reaches this branch? If the class can't be cheaply enumerated, say so in the PR rather than leaving it implied that you covered it.
- After opening or pushing to a PR, stay on it: poll CI and Bugbot on the current head and triage every finding the same day — fix it, or reply on the thread saying why not. No silent dismissals. Unresolved threads block the merge and stall the release train's settle stage; cheap now beats expensive later.
- A finding that recurs across PRs becomes a rule: add it to `.cursor/BUGBOT.md`, and if it is grep-expressible, to code-quality's house-rules — then stop re-arguing it in comments.
- Style and naming rules live in tooling (black/ruff, eslint/prettier, house-rules), never in prose. If a rule matters, encode it; do not restate linter rules in CLAUDE.md files.
- Never commit secrets, tokens, or customer data — not in code, config, tests, issues, or commit messages. gitleaks catches secrets in **code**. Nothing scans PR titles, descriptions or commit messages: the public PII gate that did was retired on 2026-08-06 (backend#1409), so keeping customer names out of PR prose on public repos is on you, not on a check.

### Engineer kanban

- Every ticket on the board carries a `Status` — no card sits at "No Status". New tickets start in `Backlog`. **Bugs are the exception:** label them `work-type:bug` (the Bug template does it) and automation moves the card straight into `Ready` — defects don't wait for refinement. Three repos aren't wired for the label trigger yet (`.github`, `release-train`, `rfcs`); move the card yourself there.
- Picking up work: the team coordinates. `Ready` is the refined queue — bugs excepted, per the line above — and the first choice when it's stocked; pulling from `Backlog` is normal when refinement hasn't caught up — say what you're taking.
- Merging to `develop` moves the card to `On dev` automatically; there is no dev-side review.
- Functional review happens once, on staging: when it passes, comment `/fr-pass` on the PR or drag the card to `Ready for prod`. Self-signoff is allowed.
- `fr-gate` is a required check on promotions. If it blocks, the board or the work isn't ready — fix that. `skip-fr-gate` is audited, for emergencies only.

### Releases & publishing

- The release train is the only path to `staging`, `main`, and every package registry. Never hand-cut a `v*` tag, hand-bump a version file, or publish an artifact — every legal publish path is inventoried in release-train's `PUBLISH-PATHS.md`.
- Findings on a promotion PR are fixed on the source branch (`develop`/`staging`), then the train re-prepares. Never push fixes onto a promotion PR — every push re-rolls its review.

### Filing issues

- Internal work — planning, epics, security findings, infrastructure, anything mentioning a customer — is filed in `backend` (the private catch-all), never in a public repo. When in doubt: `backend`.
- Public repos (`cli`, `client`, `docs`, `data-ingestors`, `model-zoo`, `start-training`, `.github`) only get issues a stranger could act on: about the public artifact itself, with no customer names, internal URLs, or internal paths.

### AI-assisted sessions (Claude Code, etc.)

- An AI session may open PRs and push its own branches. It never: merges a PR, closes another person's PR, deletes another person's branch, or force-pushes — each of those needs an explicit instruction from the human running it.
- If your change makes a statement in any CLAUDE.md, BUGBOT.md, or runbook false, update that file in the same PR.
<!-- org-standards:end -->
