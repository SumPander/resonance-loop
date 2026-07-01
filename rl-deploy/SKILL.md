---
name: rl-deploy
description: Run the Resonance Loop as a FULL CI/CD pipeline THROUGH deploy — discovery → positioning → four-axis → design → gate → shadow build → analyze → converge → deploy-bless → APPLY (live, reversibly) → VALIDATE (re-run + observe vs intent) → keep-or-revert → feed-forward. Use when you intend to SHIP a change into the live system. The deploy-bless is the act, not the approval. Provides the roles + two human gates, shadow-verify-before-live, reversible/backed-up apply, and post-deploy validation. Companion to /rl-theory.
---

# Resonance Loop — Deploy mode (full pipeline)

The complete Resonance Loop, run **through** its terminal act: a change proven against the architecture, shipped reversibly, and validated live. This is the CI/CD pipeline — the deploy-bless *triggers* apply → validate → feed-forward; it is not permission to build later.

> **Intent, one breath: build toward better — simply, and confidently.**
> The rigor exists to *earn the confidence to act*, then act. A blessed change that never ships has the same disease as analysis that never builds.

## When to use
- You intend to ship a real change into the live system this pass.
- A `/rl-theory` finding is ready to become a live change (hand it in with its convergence record).
- Any increment where "done" means *integrated + validated live*, not a proven design.

## The flow (full pipeline)

```
discovery (+ field/SOTA)  →  positioning  →  four-axis  →  design + reverse-review
   →  GATE  →  build SHADOW / isolated  →  analyze (verify + meaning re-check)  →  converge
   →  final eval  →  human DEPLOY-BLESS  →  APPLY (live, reversibly / backed up)
   →  VALIDATE (re-run + observe vs intent, with the system's own instruments)
   →  keep or REVERT  →  feed the finding forward ↻
```

A **side-store** feeds every step fresh — never relayed.

## Roles
| Role | Holds | Must not |
|---|---|---|
| **Overseer** | The *why*, laws, four axes, output; the convergence record; the final eval; **executes the deploy on bless.** | Build. Skip positioning. Deploy without the bless. |
| **Builder** | The blessed design + gate checklist; builds shadow first, then applies the blessed change reversibly. | Decide architecture. Touch live before design-bless. Apply without a backup. |
| **Strategist** | Field / SOTA; candidates; kept loose, outside pass/fail. | Converge too early. |
| **Analyzer** | Laws + positioning + four-axis + the verify harness. Pre-build AND post-deploy: does it verify clean AND still mean what was intended? | Reduce to a checklist; render the human's judgment alone. |
| **Human — 2 gates** | **Design-bless** (nothing touches live until then) + **deploy-bless** (the trigger of the act). | — |

## The two disciplines (unchanged) + the terminal motion
Positioning, four-axis, the pathway gate (reuse-vs-branch with evidence), side-store-not-relay, observe-first, both-directions, shadow-before-live, foundation-utilization, the remediation caveat — all as in [`METHODOLOGY.md`](../METHODOLOGY.md). What deploy-mode adds is the **terminal motion the bless triggers**:

- **Apply** — make the change live, **reversibly**: a backup / rollback path exists *before* you touch it.
- **Validate** — re-run / re-awaken and **observe the real behavior against the intent** (not "it imports"): does it do what was intended, is the system healthy, did anything regress? Use the system's own instruments.
- **Keep or revert** — clean → it stands; not clean → revert (the backup is why you can), and the failure is the next finding.
- **Feed forward** — what the validation surfaces becomes the next evidenced increment. Build → learn → feed back → build the next.

## The convergence record (write it before you build)
Before the first build iteration the Overseer records: **mode** (ship / refine / optimize), **"done looks like: ___"** (the checkable end-state), and an **iteration budget + escalation** (at budget → force-escalate to the human gate: *"unresolved axis = ___, or I'm over-refining"*). A re-loop that can't name a *newly*-unresolved axis is auto-converged.

## Definition of done (deploy mode)
Done when all three hold: **it fits** (output closes back in), **it means what was intended** (four-axis re-check), and **it is verified clean live** (validation green + a live observation shows the system healthy with it). "Done" = *integrated and doing what was intended*, not merely "it runs" — and, in this mode, *shipped and validated*, not merely designed.

See [`METHODOLOGY.md`](../METHODOLOGY.md) for the full depth (§6a–e cover convergence, refinement-vs-purity, the mode switch, the convergence record, and Deploy & Validate).
