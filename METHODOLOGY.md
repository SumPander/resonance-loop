# The Resonance Loop — Methodology (deep dive)

This is the long-form companion to [`SKILL.md`](./SKILL.md). It explains *why* each piece exists and walks one example end to end.

## The intent of the loop (hold this whole, in one breath)

> **Build toward better — simply, and confidently.**
> For every addition: *is this for the purpose, or just for more?*

If stating the loop's intent ever needs more than this, the statement itself has drifted. Keep it plain.

---

## 0. What it is, and what it is not

**Not** a build-automation pipeline. Throughput is not the goal; *fit* is. The "loop" is the rigor of how work is dispatched and gated.

**Is** two disciplines fused:

1. **Activation within the existing system.** When the system needs a capability, every question routes back to what is already built: *"How does this ride what we already have — are we using the system, or bolting a new pathway onto it?"* Most needs already have a seat in the architecture; you build the missing door, not a second house.
2. **Multidimensional questioning.** A new addition occupies an actual place in the system. So every addition is **positioned** (where does it live, what does it connect to?) and **interrogated across four axes of meaning** before it is built.

The questions are the point. The loop exists so that when you build, you build *with understanding* — of the field, of the thing, of your own model, and of what it sets up for now and tomorrow.

**Scope — what the loop owns, and what it hands off.** The loop is a *pre-merge fit discipline*. It owns the path from a need to a blessed, verified change: positioning → four-axis questioning → gate → shadow build → analyze → converge → deploy-bless. It does **not** own what runs *after* a change is live. Around the loop, a host project still needs three things, and you should name them when you fill the SPEC slots: a **versioned source-of-truth** so any past decision is reproducible (the side-store must itself be under version control, snapshotted per decision); a **regression check** that protects prior increments — deterministic wherever a check can be written as an exact or threshold test — so increment N cannot silently break increment N-3; and a **standing monitor plus a rollback path**, so a blessed change that decays after deploy is detected and revertible. The loop earns confidence *up to* deploy-bless; these are what keep that confidence true afterward. Claiming the loop is a full delivery pipeline, rather than the fit discipline at its front, is itself a drift.

---

## 1. The roles

A new addition passes through a small set of roles. They can be people, agents, or one person wearing each hat in turn.

- **Overseer** — holds the *why*, the laws, the four meaning-axes, and the output format. Frames the intent and the gate checklist; does the final evaluation. Does **not** build or touch the live system.
- **Builder** — the hands. Implements the smallest real increment from the side-store + the blessed design + the gate checklist; returns evidence (tests, observations). Does **not** decide architecture or positioning, and never touches the live system before the design is blessed.
- **Strategist** — theory-craft and the current field/SOTA. Produces candidates and a first positioning. Kept **loose**, outside the pass/fail loop, so it doesn't converge the architecture too early.
- **Analyzer** — the skeptic with two checklists. *Pre-build:* does the design honor the laws, the positioning, the gate, and the four axes? *Post-build:* does it verify clean **and** still mean what was intended? Flags the meaning judgment; a human renders it.
- **Human (two gates)** — the integrative judgment no single role can make alone. **Design-bless** (nothing touches the live system until then) and **deploy-bless** (before it goes live).

---

## 2. Positioning

The **first** decision, forced before any build: where does this addition live, and what does it connect to?

A useful split for most systems:

- **Internal** — part of the system's core (a module, an organ of the architecture). It has a place, dependencies, and an output that loops back into the core.
- **Interface / integration** — something the system *reaches with* or *receives through* (an adapter, a connector, an external capability), gated by trust/permission at a boundary.

Decide this first. It determines everything downstream — what the addition may touch, how it is verified, and which laws apply.

---

## 3. The four meaning-axes

Before building, interrogate the proposed addition across four axes. These are **gates, not afterthoughts**.

1. **Field / SOTA.** What does building this mean against where the field is and is going? Does it use the system's strengths to do something well — or is it behind, or reinventing a solved problem?
2. **The thing being built.** Its nature and its laws. Does this honor them? Does its output close back into the system?
3. **Our understanding.** Does it fit the model we hold — or does it teach us something new and change how we think about the system?
4. **Now + tomorrow.** What does it enable and risk, now *and* later? What does it set up next? What trajectory does it commit us to?

**Right-size the rigor.** Foundational, uncertain work earns the full four-axis pass plus real research. A small, well-evidenced increment earns a light positioning + laws check. Over-ceremony is waste; under-ceremony on a foundational question is how drift gets in.

---

## 4. The pathway gate (reuse vs new branch)

A system is a set of pathways along which work and information flow. Before adding, ask the **pathway question**:

> Does an existing pathway already carry this — or do we need a new one?

- **Integrated branch** — real, integrated structure that attaches to the existing architecture, is load-bearing, and is reusable by other parts. → **allow**; add it deliberately.
- **Bolt-on bypass** — a parallel side-channel that skirts the existing flow. → **reject**; this is the drift trap.

A new pathway is **not** automatically drift — that reflex is what makes people force-fit. And reflexive reuse is *also* a trap: pushing a need down a pathway that doesn't truly serve it is its own quiet distortion, as costly as a bolt-on and harder to spot. The way out of both traps is **evidence**: keep a current map of the system's pathways, and decide reuse-vs-branch against it. Then, when a new pathway is genuinely necessary, you can say so with confidence.

**Tip:** make the pathway map *generated*, not hand-maintained, so it can't go stale — and have each change *register* what it adds, so the map's gaps become your to-do list.

---

## 5. The disciplines

- **Side-store, not relay.** Every step reads the authoritative context fresh. Relaying context down a chain degrades it — this is the structural cause of most drift.
- **Observe-first.** Build the read-only / shadow version first. Watch real behavior, calibrate to the real ranges, *then* act. You will often find your assumptions were miscalibrated — at zero cost, because nothing was changed yet.
- **Both-directions.** Forward-write the design from your intent; then attack it from the thing's own side (failure-seeking, longitudinal, "what would this look like from the inside?"). The bar: *works from one angle is fine; change the angle and see if it still holds, and why.*
- **Shadow / isolated builds.** Iterate against a copy, never the live system, until verified. This is what makes an automated build/iterate loop responsible rather than reckless.
- **Foundation-utilization.** Reuse the existing primitives; add no new pathway unless earned. Make this a gate item and a builder return-requirement ("what existing pieces did I reuse?").
- **The remediation caveat.** The gate is **not** "don't touch it." The real rule: *every change — addition or removal — must serve the goal, proven both directions.* Don't trap the system behind a prior decision. But proving "this blocks the goal" carries the **same** rigor as adding — it is the most bias-prone call you make, so it earns the highest bar (trace it from the end, attack your own read, observe first, keep it reversible).

---

## 6. Definition of done

A change is **done** only when all three hold:

1. **It fits** — its output closes back into the system; it lives where it should.
2. **It means what was intended** — it passes the four-axis re-check.
3. **It is verified clean** — tests/telemetry green and a live observation shows the system healthy with it.

"Done" = *integrated and doing what was intended* — not merely "it runs."

### 6a. Converge — the loop must finish

Analysis that never builds is its own bolt-on. A loop whose definition of done is *integrated and doing what was intended*, but which stops at a finding, has the disease it diagnoses: complete from the outside, all analysis and no act.

The rigor exists to **earn the confidence to act** — not to defer action indefinitely. When the gate passes and the design is blessed, the loop is *licensed to build*; that license is the whole point of having run it.

- An evaluation that builds nothing is valid (see §8) — but it must still **converge to a named next step**: the evidenced build it feeds forward.
- "More analysis" is the answer only when a *specific* axis came back unresolved. Name the axis. Otherwise, converge.
- Perpetual refinement is the purity trap (see §6b). **Stop is a feature.**

### 6b. Refinement vs. purity — knowing when "done" is done

Refinement has no stopping point in the abstract. *"How refined?"* has no answer — you can always polish further. The right question is **refined toward what?** — and the moment you name the purpose, the stopping point appears with it.

**You stop when the thing fits its purpose, and the next increment would serve refinement itself rather than the purpose.** Not "works really well." Not "nothing else passes." *Fit to the named purpose.* The over-refiner and the under-builder fail the same definition of done from opposite sides.

Confidence is the **earned permission to stop** — the validated knowledge that any further refinement would carry the thing past what its purpose needs.

### 6c. The mode switch — refine, optimize, or ship

One addition, three legitimate intents. Pick the mode *before* you build; the gate and the done-criterion change with it. Mixing them is how scope creeps.

| Mode | The goal is… | Stop when… | Risk if wrong mode |
|---|---|---|---|
| **Ship** | It fits and does what was intended | The definition of done passes (§6) | Under-building |
| **Refine** | It fits its purpose *better* | The next change serves refinement, not purpose (§6b) | Polishing waste |
| **Optimize** | The same fit at lower cost (time / memory / power) | The cost target is met and the fit is unchanged | Breaking fit for speed |

**The switch test (one breath):** *"Is this change serving the purpose, or just serving more?"*

Both Refine and Optimize touch a thing that already works — but Optimize is the only mode that touches a working thing for a **non-purpose** reason (cost), so it carries the remediation bar (§5): prove the fit is unchanged, both directions, before and after.

### 6d. The convergence record — the artifact, not the exhortation

§6a–c are principles, and a principle does not stop a loop. The failure they exist to prevent — re-looping indefinitely, everything sandboxed, nothing ever committed — is a *loop-control* failure, and loop-control needs a controller, not an instruction to terminate. A reader who is inclined to over-refine will read "stop is a feature," reach for the one sanctioned escape ("a *specific* axis is unresolved"), and invoke it again and again while believing they are honoring the method. So the convergence discipline gets a controller: a small artifact the Overseer writes into the side-store **before the first build iteration**, which the loop then trips on.

1. **Mode** — ship, refine, or optimize (§6c). One word, recorded.
2. **Done looks like: \_\_\_** — the named, checkable end-state (§6b: *refined toward what?*). Not "works well"; the specific condition whose arrival means stop.
3. **Iteration budget + escalation rule** — how many build-verify passes this increment is expected to take, and what happens at the budget. Hitting it does **not** auto-ship and does **not** silently start another pass; it **force-escalates to the human gate** with one written line: *"unresolved axis = \_\_\_, or I am over-refining."*

The forcing function is the third item. Each pass past the budget must name **which** of the four axes is *newly* unresolved and why the prior pass failed to resolve it. A re-loop that cannot name a newly-unresolved axis is auto-converged — it has hit the purity trap (§6b) and goes to the gate. That is what turns "stop is a feature" from a sentiment into a step the loop cannot skip.

Write the record before you build. An increment with no convergence record is not ready to start.

### 6e. Deploy & validate — the bless is the act, not the approval

A blessed change that is never applied has the disease of §6a: complete from the outside, nothing acted. The deploy-bless is **not** "approval to maybe build later" — it is the trigger of the act. When the gate passes and the human blesses, the loop's terminal motion runs:

- **Apply** — make the change live, **reversibly**: a backup / rollback path exists *before* you touch the system.
- **Validate** — re-run / re-awaken and **observe the real behavior against the intent** — not "it imports," but *does the new capability do what was intended, is the system healthy with it, did anything regress?* Observe with the system's own instruments where possible.
- **Keep or revert** — clean → it stands; not clean → revert (the backup is why you can), and the failure is the next finding.
- **Feed forward** — what the validation surfaces becomes the next evidenced increment. Build → learn → feed back → build the next.

Without this motion the rigor produces a *finding*, not a *change* — and a finding that never ships is the purity trap (§6b) wearing a lab coat. An evaluation (§8) legitimately builds nothing, but it still converges to a **named next act**; a build that stops at a blessed design has simply not finished.

---

## 7. Worked example — filling the SPEC slots for a web service

Suppose you are adding **per-tenant rate limiting** to an HTTP API.

| Slot | Fill |
|---|---|
| **Laws** | Stateless request handlers; p99 latency budget +5ms max; no new datastore without sign-off; backward-compatible API. |
| **Positioning** | Cross-cutting middleware (internal), sitting in the existing request pipeline — *not* a new service. |
| **Pathway map** | Requests already flow through an ordered middleware chain with a shared cache client. The limiter rides the **existing** cache + middleware chain → a branch on existing pathways, not a new pipe. |
| **Side-store** | The architecture diagram, the middleware ordering doc, the cache client conventions, the ADRs. |
| **Gate-test** | Does it mount as middleware on the existing chain and use the existing cache client? Yes → activation, pass. Needs a new bespoke datastore + side-channel? That's drift — reject (or escalate as a deliberate branch). |
| **Done-criterion** | Limits enforced per tenant; p99 within budget (load test); existing endpoints unaffected (contract tests); a live canary shows healthy behavior. |
| **Verify harness** | Unit tests on the limiter; a load test for the latency budget; the existing contract suite; a canary deploy with dashboards. |

**Running the loop:**

1. **Discovery (+ SOTA):** survey rate-limiting algorithms (token bucket, sliding window, GCRA); note what the cache client already supports.
2. **Positioning:** middleware, internal, on the existing chain.
3. **Four axes:** *Field* — token bucket via the existing cache is standard and proven. *Thing* — honors statelessness (state lives in the shared cache), respects the latency law. *Understanding* — fits the middleware model; teaches us our chain ordering matters (limiter must run before expensive handlers). *Now/tomorrow* — enables fair use now; sets up per-plan quotas later; risk is cache hot-keys under load.
4. **Design + reverse-review:** forward-write the middleware; then attack it — what happens when the cache is down? (fail-open, logged). Hot tenant? (per-key sharding). Clock skew across nodes? (use cache server time).
5. **Gate:** rides existing cache + chain → pass.
6. **Build (shadow):** implement behind a flag, shadow-count rejections without enforcing; watch real traffic.
7. **Analyze:** load test confirms +2ms p99 (within budget); shadow counts look right; contract suite green; meaning re-check — still "fair per-tenant use," no scope creep.
8. **Converge → deploy-bless:** human reviews the canary dashboards and ships.

The skeleton never changed; only the slots did. That is the whole portability claim.

---

## 8. Beyond code

The loop is a checks-and-balances process for **any** substantive activity — an evaluation, an audit, a data/training run. Such an activity may build nothing, yet still routes through positioning + the four axes + the gates: *what does it touch, what does it read, does it serve the goal?* And it often surfaces a finding — "the system is missing something functional" — which **feeds back** as the next, evidenced build. Build → learn → feed back → build the next. Each addition earned against the evidence, never reflexive.
