# The Resonance Loop — Methodology (deep dive)

This is the long-form companion to [`SKILL.md`](./SKILL.md). It explains *why* each piece exists and walks one example end to end.

---

## 0. What it is, and what it is not

**Not** a build-automation pipeline. Throughput is not the goal; *fit* is. The "loop" is the rigor of how work is dispatched and gated.

**Is** two disciplines fused:

1. **Activation within the existing system.** When the system needs a capability, every question routes back to what is already built: *"How does this ride what we already have — are we using the system, or bolting a new pathway onto it?"* Most needs already have a seat in the architecture; you build the missing door, not a second house.
2. **Multidimensional questioning.** A new addition occupies an actual place in the system. So every addition is **positioned** (where does it live, what does it connect to?) and **interrogated across four axes of meaning** before it is built.

The questions are the point. The loop exists so that when you build, you build *with understanding* — of the field, of the thing, of your own model, and of what it sets up for now and tomorrow.

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
