# Autopsies — why dead targets died (anonymized)

I write a post-mortem for every target that yields nothing, *before* opening the next one. Kept together,
they reveal patterns across targets — which is the point. Names are generalized to archetypes; no
vulnerabilities are disclosed (none were found in these). All testing was under program rules of
engagement, on my own accounts.

## Track record, honestly
Seven targets, zero findings at the time of writing. Six were shallow passes I bailed on too early; the
seventh was a genuine deep dive that still returned nothing — which taught me the most (see Lesson 5).
I'm publishing the misses because the *analysis* of them is the skill I'm building.

## The targets (by archetype)
| # | Archetype | Depth reached | One-line cause of death |
|---|---|---|---|
| 1 | Open-core API gateway (infra) | shallow | security-critical infrastructure; dropped at selection |
| 2 | Hardened security plugins of a CI system | medium | scope was the vendor's own hand-picked, hardened code |
| 3 | Closed-source Electron API client | medium | the dangerous primitive wasn't reachable; key path already publicly disclosed |
| 4 | Popular open-core collaboration platform | med-deep | public repo + active bounty = already read and pre-hardened |
| 5 | Closed-source Electron productivity app + backend | deep | well-resourced vendor hardened both client and backend |
| 6 | File-sharing SaaS REST API | shallow | free-tier authz was solid; the interesting vectors were paywalled/reputation-gated |
| 7 | Mature retail commerce backend (GraphQL over legacy) | deep | ~3-yr program on a decades-mature authz layer = swept; rich vectors gated behind a purchase |

## Patterns — what the post-mortems taught me
**1. Source availability kept driving selection into swept classes.** I repeatedly picked targets *because*
the source was readable (open-core infra, public OSS). For those classes, readable source is a reason they
are *more* hunted, not less. Fix: stop letting "I can read the code" select the target.

**2. Depth was the through-line of the early failures.** Several targets I closed after ~20 requests and
called "hardened." That's a shallow-pass reflex, not a conclusion. Fix: a commitment device — don't move
on until genuinely out of hypotheses.

**3. Closed-source ≠ automatically less-swept.** A closed-source desktop client from a well-resourced
company was as hardened as its backend. The reversing edge only pays when the vendor is *also* newer /
less-security-mature / product-focused.

**4. "Reachable ≠ interesting" — the most expensive recurring mistake.** Twice I cleared free signup, then
spent the session on the hardened free slice while every business-logic-rich vector sat behind a paywall,
a reputation wall, or a required purchase. Now it's a written pre-commit checklist: map which high-value
vectors are gated *before* investing, and either plan to reach them or walk.

**5. Depth is necessary but not sufficient — selection is the binding constraint.** My one real deep dive
(full API map from client bundles, two-account dynamic authorization testing, a false-positive caught by
my own verification gate) was executed well and still found nothing, because the target was mis-selected:
a mature backend on a decades-hardened authorization layer. The method worked; the pick was wrong. Lesson:
once you can go deep, the leverage moves to picking a target *worth* the depth.

**6. Enforce the triage timebox.** In that deep dive I burned ~20 steps rabbit-holing one speculative
vector against my own "log it and move on" rule. Discipline candidate: unconfirmed in ~5 minutes → back to
the ranked queue.

## Why I keep these
A post-mortem that just shrugs "hardened" produces zero systemic lessons. Forcing myself to name the
specific cause, the knowledge gap, and the tooling gap is what turns seven zeros into a sharper process.
