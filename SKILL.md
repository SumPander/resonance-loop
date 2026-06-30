---
name: resonance-loop
description: A disciplined methodology for bringing any new capability into any system without architectural drift. Use when adding a feature, integration, or capability and you want it to fit the existing architecture with evidence — not bolt it on. Provides roles (Overseer / Builder / Strategist / Analyzer + two human gates), a positioning step, four-axis questioning, a reuse-vs-new-pathway gate, observe-first shadow builds, and a definition of done that means "fits and does what was intended," not merely "runs." Works solo or as a multi-agent harness.
---

# The Resonance Loop

A process for adding capability to a system so that **every addition fits** — proven against the architecture, not bolted on. It works whether one person wears every hat in sequence or several agents run the roles in parallel. The value is the discipline, not the headcount.

Two disciplines, fused into one loop:

1. **Activation within the existing system.** Before adding anything, ask whether the system *already* does this. Most "new" needs have a seat in what's already built. Reuse the existing primitives; add a new pathway only when one is genuinely earned.
2. **Multidimensional questioning.** Every addition is *positioned* (where does it live?) and *interrogated* across four axes of meaning *before* it is built. The questions are the point — they guarantee you build with understanding.

## When to use

- Adding a feature, integration, module, or capability to an existing system.
- Any time you feel the pull toward a quick bolt-on and want a check against drift.
- Evaluations, audits, or training/data runs that build no code but still need checks-and-balances (see **Universal**, below).

## The roles

| Role | Holds | Asks | Must not |
|---|---|---|---|
| **Overseer** | The *why*, the laws, the four meaning-axes, the output format. Does the final eval. | The meaning-questions and the positioning call, up front. | Build. Touch the live system. Skip positioning. |
| **Builder** | The blessed design, the gate checklist, the authoritative context (read fresh). | "What's the smallest real increment, and does it pass the gate?" | Decide architecture/positioning. Touch the live system before the design is blessed. |
| **Strategist** | The docs, the probes, **and the current state of the field / SOTA**. | "What does the field know? What candidates exist? Where might this sit?" | Get pulled into pass/fail too early (premature convergence). |
| **Analyzer** | The laws, the positioning decision, the four-axis intent, the verify harness. | Pre-build: "Does the design honor the laws + positioning + gate + the four axes?" Post-build: "Does it verify clean AND still *mean* what we intended?" | Reduce to a checklist. Make the *meaning* judgment alone — flag it; a human judges. |
| **Human (×2 gates)** | Everything. | "Is this the right thing? Do I bless this design? Do I bless this deploy?" | — |

*Solo:* one person/agent wears all the hats in sequence. Keep the two human gates real even then — they are where the integrative judgment lives.

## The flow

```
discovery (+ field/SOTA)  →  positioning  →  four-axis questioning  →  design + reverse-review
   →  GATE  →  build (shadow / isolated)  →  analyze (verify + meaning re-check)
   →  converge  →  final eval  →  human deploy-bless
```

A **side-store** — the authoritative context (architecture map, design docs, the laws) — feeds **every** step fresh. Never relay it down a chain; relaying degrades it. This is the structural fix for drift.

## The four meaning-axes (asked as gates, not afterthoughts)

1. **Field / SOTA** — what does building this mean against where the field is and is going? Ahead, aligned, or behind?
2. **The thing being built** — its nature and its laws. Does this honor them? Does its output close back into the system?
3. **Our understanding** — does it fit the model we hold, or teach us something new and change how we think?
4. **Now + tomorrow** — what does it enable and risk, in the present *and* the future? What trajectory does it commit us to?

Right-size the rigor: foundational, uncertain work gets the full four-axis pass plus deep research; small, well-evidenced increments get a light positioning + laws check. Over-ceremony is waste; under-ceremony on a foundational question is drift.

## The pathway gate (reuse vs new branch)

Before adding, ask the **pathway question**: *does an existing pathway already carry this — or do we need a new one?*

- **Integrated branch** — real, integrated structure: it attaches to the existing architecture, is load-bearing, and other parts can use it. → **allow** (add it deliberately).
- **Bolt-on bypass** — a parallel pipe (a custom side-channel) that skirts the existing flow. → **reject** (the drift trap).

A new pathway is **not** automatically drift. But reflexive reuse is *also* a trap: forcing a need onto a pathway that doesn't truly serve it is its own quiet distortion — as costly as a bolt-on, and harder to see. Choose reuse-vs-branch with **evidence** — a current map of the system's pathways — so you can say, with confidence, when a new one is genuinely necessary.

## Universal disciplines

- **Side-store, not relay** — every step reads the authoritative context fresh.
- **Observe-first** — build the read-only / shadow version, watch real behavior, calibrate, *then* act.
- **Both-directions** — forward-write the design, then attack it from the thing's own side (reverse-review). "Works from one angle" is not enough; change the angle and see if it still holds.
- **Shadow / isolated builds** — iterate against a copy, never the live system, until verified. This is the safety primitive that makes an automated build/iterate loop responsible.
- **Foundation-utilization** — reuse the existing primitives; add no new pathway unless genuinely earned. (A gate item; the builder must report what it reused.)
- **The remediation caveat** — the gate is not "don't touch it." The rule is: *every change — addition OR removal — must serve the goal, proven both directions.* Don't trap the system behind a prior decision; but proving "this blocks the goal" carries the **same** rigor as adding (it is the most bias-prone call you make).

## The SPEC slots (fill these per project)

| Slot | What it is |
|---|---|
| **Laws** | The non-negotiable spec the gate checks against (architecture conventions, budgets, invariants). |
| **Positioning** | Where a new addition can live (internal module vs external interface/integration). |
| **Pathway map** | The system's existing integration points + the branch-vs-bypass test. |
| **Side-store** | The authoritative context every step reads (architecture map, design docs, decision records). |
| **Gate-test** | The concrete pass/reject question (fits-existing-architecture vs introduces-drift). |
| **Done-criterion** | When it is truly finished: *fits + means-what-intended + verified clean* — not merely "runs." |
| **Verify harness** | How you watch the built thing behave (tests, telemetry, a live smoke run). |

The skeleton above is constant across projects; only the slots change.

## Definition of done

A change is **done** when all three hold:

1. **It fits** — its output closes back into the system; it sits where it should.
2. **It means what was intended** — it passes the four-axis re-check.
3. **It is verified clean** — tests/telemetry green and a live observation shows the system healthy with it.

"Done" = *integrated and doing what was intended* — not merely "it runs."

## Universal — beyond code builds

The loop is a checks-and-balances process for **any** substantive activity, not only code. An evaluation, an audit, or a training/data run builds nothing, yet still routes through positioning + the four axes + the gates: *what does it touch, what does it read, does it serve the goal?* Such an activity often surfaces a finding — "the system is missing something functional" — which **feeds back** as the next, evidenced build. Build → learn → feed back → build the next: each addition earned, never reflexive.
