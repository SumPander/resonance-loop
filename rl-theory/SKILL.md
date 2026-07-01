---
name: rl-theory
description: Run the Resonance Loop in THEORY / TEST-BENCH mode — the full rigor WITHOUT shipping. Use for exploration, design passes, evaluations, audits, or observe-first dry-runs where you want a proven design or finding but must NOT touch the live system. Deploy is OFF: the loop converges to a named next step that /rl-deploy can then execute. Provides the roles (Overseer / Builder / Strategist / Analyzer + the design-bless human gate), positioning, four-axis questioning, the reuse-vs-branch gate, shadow / observe-first builds, and the convergence record. Companion to /rl-deploy.
---

# Resonance Loop — Theory / Test-Bench mode (deploy OFF)

The Resonance Loop with the **deploy stage disabled**. Same rigor, no live change. Use it to think a change all the way through, prove it against the architecture, and *test-bench* it against a shadow copy — then stop at a converged finding you can hand to **`/rl-deploy`**.

> **Intent, one breath: build understanding toward a change worth making — simply, and confidently.**
> Deploy is OFF here. This mode's job is a *proven design or finding*, not a live change. It still must **converge** (a finding that never resolves is its own bolt-on) — but it converges to a **named next step**, not a deploy.

## When to use
- A design pass, spike, or exploration before you're ready to touch anything.
- An evaluation, audit, or data/observation run that builds nothing but must route through the gates.
- An observe-first / shadow test-bench: prove behavior against a copy, calibrate to real ranges.
- Any time you want the discipline but explicitly must **not** ship (no bless yet, risky surface, someone else deploys).

## The flow (stops before deploy)

```
discovery (+ field/SOTA)  →  positioning  →  four-axis questioning  →  design + reverse-review
   →  GATE  →  build SHADOW / observe-first (never live)  →  analyze (verify + meaning re-check)
   →  converge to a NAMED FINDING  ⊘ stop (hand to /rl-deploy)
```

A **side-store** — the authoritative context (architecture map, design docs, laws) — feeds every step fresh. Never relay it down a chain.

## Roles
| Role | Holds | Must not |
|---|---|---|
| **Overseer** | The *why*, the laws, the four axes, the output. Frames the convergence record; does the final read. | Build. Touch the live system. |
| **Builder** | The blessed design + gate checklist; builds **only shadow / read-only** in this mode. | Touch the live system at all (deploy is OFF). |
| **Strategist** | The field / SOTA; candidates; kept loose, outside pass/fail. | Converge the architecture too early. |
| **Analyzer** | The laws + positioning + four-axis; verifies the shadow build + the meaning. | Reduce to a checklist; render the human's judgment alone. |
| **Human — 1 gate** | **Design-bless** (is this the right thing, is the finding sound?). | — (deploy-bless is not reached in this mode) |

## The four meaning-axes (gates, not afterthoughts)
1. **Field / SOTA** — ahead, aligned, or behind? 2. **The thing** — its nature/laws; does its output close back in? 3. **Our understanding** — does it fit our model or teach us something new? 4. **Now + tomorrow** — what it enables/risks, and the trajectory it commits us to.
Right-size the rigor: foundational/uncertain work earns the full pass + research; a small increment earns a light positioning + laws check.

## The pathway gate (reuse vs new branch)
Before adding, ask: does an existing pathway carry this, or do we need a new one? **Integrated branch** (attaches, load-bearing, reusable) → allow. **Bolt-on bypass** (parallel pipe skirting the flow) → reject. Reflexive reuse is *also* a trap — decide with evidence (a current map of the system's pathways).

## Disciplines
- **Side-store, not relay** — every step reads the authoritative context fresh.
- **Observe-first** — build the read-only / shadow version, watch real behavior, calibrate, *then* (in /rl-deploy) act.
- **Both-directions** — forward-write the design, then attack it from the thing's own side.
- **Shadow / isolated only** — this mode iterates against a copy and never the live system.
- **Foundation-utilization** — reuse existing primitives; report what you reused.

## The convergence record (write it before you build — even here)
Principles don't stop a loop; an artifact does. Before the first shadow build, the Overseer records: **mode** (here: *theory / test-bench*), **"done looks like: ___"** (the specific finding / proven design), and an **iteration budget + escalation** ("name the unresolved axis or converge"). A re-loop that can't name a *newly*-unresolved axis is auto-converged.

## Definition of done (theory mode)
A theory-mode pass is **done** when it **converges to a named next step**: a blessed design, a proven-in-shadow finding, or an evidenced build proposal — *and names what /rl-deploy would ship.* It is NOT done if it stops at "interesting" with no named next act. **Stop is a feature; drift is stopping short of a named finding.**

## Handoff
When the finding is ready to become a live change, hand it — with its convergence record — to **`/rl-deploy`**, which runs the full pipeline through apply → validate → feed-forward. See [`METHODOLOGY.md`](../METHODOLOGY.md) for the deep dive.
