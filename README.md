# Bug-Bounty Methodology & Field Notes

A public, sanitized subset of my working notes as a web-application vulnerability researcher.
It documents **how I pick targets, hunt, verify findings, and learn from dead ends** — the process,
not any live or unreported work.

> **Scope & ethics note.** Everything here is method and generalized lessons. Details of active targets,
> account data, and any unreported research are deliberately excluded. Past targets are anonymized by
> archetype (e.g. "a file-sharing SaaS") rather than named, and no vulnerabilities are disclosed here.
> All testing referenced was performed under the relevant program's rules of engagement, on my own
> accounts, without accessing other users' data.

## Why this exists
Most beginners spray automated scanners at well-hunted programs and submit polished-but-duplicate reports.
I'm deliberately building the opposite habit: **understand one application deeper than the crowd bothered
to, and attack its own business-logic assumptions** — the class of bug that survives automated sweeps.

## What's inside
- **[METHODOLOGY.md](METHODOLOGY.md)** — my operating process: target-selection gates, the depth-first
  deep-dive method, per-target mapping, a verification/duplicate gate, and rules-of-engagement discipline.
- **[AUTOPSIES.md](AUTOPSIES.md)** — post-mortems on targets that yielded nothing, anonymized. The point:
  I write down *why* a hunt failed and roll recurring lessons back into the method. Honest failure analysis
  is the fastest way I know to improve.

## Where I am
Early-stage and honest about it: I'm in my first months of bug-bounty research, building a track record.
These notes are the discipline I'm bringing to that climb. Feedback welcome.
