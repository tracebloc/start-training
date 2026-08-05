# Bugbot guide — tracebloc/start-training

## Context

A Jupyter notebook quick-start (Colab or local) that walks a user through launching
a tracebloc training experiment with the `tracebloc` SDK: connect, upload a model,
link a dataset, configure, start. Public repo, Apache-2.0.

## Known non-issues — do not flag

- A `code-quality-caller.yml` that passes **no `secrets:` line** is correct, not an omission.
  The shared `code-quality.yml` reusable references no secrets by contract
  (RFC-BACKEND-1405 Q5, backend#1526): secretless callees get no secrets line, and if the
  reusable ever gains one, callers switch to explicit per-secret passing — never
  `secrets: inherit`. Flag the *addition* of `secrets: inherit` on this caller instead.

## Tone

Direct. Name the file and line. Give a concrete fix, not "consider".

This repo is **public**: never put a customer name, internal hostname, or internal-only ticket detail in a finding. A bare `tracebloc/backend#NNNN` reference is fine.

## Working with Bugbot findings (team norm)

Every Bugbot review thread gets a reply, then gets resolved:
- **Fixed**: say what changed and in which commit.
- **False positive**: say why, with evidence (file/line, measured behavior).
Unresolved cursor threads HOLD release-train promotions (soft gate) — an
unaddressed finding blocks the fleet, not just this PR.
