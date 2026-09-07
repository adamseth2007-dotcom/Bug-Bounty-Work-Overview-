# Methodology

My operating process for authorized web-application bug-bounty research. Distilled from working notes;
generalized so it names no live target.

## Mission
Get a genuine, reproducible, *payable* finding on the board — optimizing for
**expected value = payout × probability-of-a-novel-valid-finding**, not raw payout or report volume.
One real reproducible bug beats a stack of polished duplicates.

## The core belief
My edge is not reading source code or running tools everyone runs. It's **understanding one application
more deeply than the crowd bothered to**, then attacking its own assumptions. Standard, by-the-book
attacks (flat IDOR, reflected XSS, enumeration) are already swept on any active program; non-standard
attacks are the *output* of deep understanding, not a trick sprinkled on top.

## Step 0 — cheap kills before investing an hour
Two 30-second checks, done first:
1. **Reachability** — can I actually create the test accounts the hunt needs (email-only signup, no
   hard geo/phone/KYC wall)? If not, the target is dead on arrival regardless of how interesting it is.
2. **Pays cash, live** — confirm a current cash reward grid (not points/VDP) and that the scope I can
   reach is eligible.
3. **Reachable ≠ interesting** — passing signup is not enough. Before committing, I write down which
   high-value vectors (payments, multi-user interactions, admin/role features) are actually reachable on
   the tier I have, versus paywalled/reputation-gated. If the *interesting* surface is out of reach, I
   walk away rather than spend the session testing the hardened free slice.

## Target selection
**Prefer:** newer / less-security-mature programs; freshly-added scope or brand-new features (fresh code,
fewer eyes); business-logic-rich domains (marketplace, fintech, booking, billing, multi-tenant SaaS);
apps that do something non-standard or domain-specific (fewer hunters understand them deeply); a slow
trickle of resolved reports (the crowd got bored and left) over hundreds-resolved with sub-day triage.

**Avoid:** security-critical infrastructure (gateways, IAM, sandbox libraries) and security vendors —
the most-hardened, most-hunted code, smallest pool; mega-programs with years of history and thousands of
resolved reports; flat static bugs on well-hunted apps (already swept).

## The method — one target, deep
Depth over breadth. Per target I build a small set of notes:
- **overview** — what the app does, who the users/roles are, how money and state move.
- **attack-surface** — endpoints, inputs, roles/tiers, and especially the **trust boundaries** where the
  server is *supposed* to enforce a rule.
- **hunt-log** — a running, *ranked* queue of hypotheses, each with what I tried and what came back.

Mapping is a **loop, not a waterfall**: map a feature → it raises a "what if…" → test it → the response
teaches something the docs didn't → update the map → new hypotheses. Every mapped feature must output an
attack idea ("what would have to be true for this to be broken?"). A purely factual note is a wiki, not a
hunting tool.

**Triage discipline:** separate *generating* hypotheses from *executing* them. If a hypothesis confirms in
a few minutes, fire it; otherwise log it and keep mapping, then periodically force-rank by
likelihood × impact × effort and work high-likelihood / low-effort first. Don't rabbit-hole the first
shiny idea while a trivial flaw sits unmapped elsewhere.

**Commitment device:** don't abandon a target as "hardened" after a shallow pass. Keep generating and
testing hypotheses until genuinely out of ideas.

## Verification / duplicate gate
Nothing becomes a report until it passes both:
1. **Dup-check** — search public advisories, CVEs, changelogs, and disclosure feeds for the exact class.
2. **Adversarial review** — red-team my own finding ("why is this a duplicate / by-design / a
   false-positive?").

## Reporting
Match the program's template exactly; one vulnerability per report; an undeniable, reproducible
proof-of-concept is the currency. Polish is not the edge — programs are drowning in well-formatted
duplicate reports. The reproduction is what pays.

## Rules of engagement (non-negotiable)
Test only accounts I own. Never access, modify, or export other users' data — if I ever encounter real
sensitive data, I stop that vector immediately, don't save or share it, and report it. Respect scope and
rate limits; no denial-of-service, no social engineering, no bot-detection/CAPTCHA bypass. When a step is
sensitive, a human performs it and stays in the loop.

## Learn from the dead ends
Every closed target gets a written post-mortem before I open the next one: why the hunt failed, what
knowledge gap it exposed, what tooling gap it hit. Recurring lessons get rolled back into this document.
See [AUTOPSIES.md](AUTOPSIES.md).
