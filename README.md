# Resonance Loop

**A disciplined methodology for adding capability to any system without architectural drift.**

Every addition should *fit* — proven against the architecture, not bolted on. The Resonance Loop is a small set of roles, gates, and disciplines that make "does this belong, and does it actually do what we intended?" a question no change can skip. It runs solo (one person/agent wearing every hat in sequence) or as a multi-agent harness.

It is **not** a build-automation tool. The "loop" is the rigor of how work is dispatched and gated — not push-button automation.

## Why

Most systems don't rot from one bad decision; they rot from a hundred reasonable-looking bolt-ons, each of which *almost* fit. The Resonance Loop attacks that directly:

- **Reuse before you add.** Most "new" needs already have a seat in what's built. The pathway gate forces the question: does an existing pathway carry this, or do we genuinely need a new one?
- **Question before you build.** Every addition is positioned and interrogated across four axes of meaning *before* a line is written.
- **Both directions.** Forward-write the design, then attack it from the thing's own side. "Works from one angle" is not enough.
- **Observe-first, shadow always.** Build the read-only version, watch real behavior, calibrate, *then* act — against a copy, never the live system, until verified.
- **Two human gates.** Nothing touches the live system until a human blesses the design; nothing ships until a human blesses the deploy.

## Use it as a skill (slash command)

This repo ships as a portable agent **skill**. With a compatible agent/CLI (e.g. Claude Code), drop the skill in and invoke it:

```
/resonance-loop
```

**Install:** copy [`SKILL.md`](./SKILL.md) into your agent's skills directory as `resonance-loop/SKILL.md` (for Claude Code: `~/.claude/skills/resonance-loop/SKILL.md`, or add this repo as a plugin). The skill is self-contained — the front-matter `description` tells the agent when to reach for it.

You can also just **read it.** [`SKILL.md`](./SKILL.md) is the concise operating guide; [`METHODOLOGY.md`](./METHODOLOGY.md) is the deep dive with a fully worked example.

## The shape, in one screen

```
discovery (+ field/SOTA)  →  positioning  →  four-axis questioning  →  design + reverse-review
   →  GATE  →  build (shadow / isolated)  →  analyze (verify + meaning re-check)
   →  converge  →  final eval  →  human deploy-bless
```

A **side-store** (the authoritative context) feeds every step fresh — never relayed down a chain.

**Roles:** Overseer (the *why*, the gates) · Builder (the smallest real increment) · Strategist (discovery + field/SOTA) · Analyzer (the skeptic, two checklists) · Human (two gates).

**The four meaning-axes:** field/SOTA · the thing being built · our understanding · now + tomorrow.

**Definition of done:** *fits + means what was intended + verified clean* — not merely "runs."

## Make it yours (the SPEC slots)

The skeleton is constant; you fill seven slots per project:

| Slot | What it is |
|---|---|
| Laws | The non-negotiable spec the gate checks against |
| Positioning | Where a new addition can live (internal vs interface) |
| Pathway map | The system's integration points + branch-vs-bypass test |
| Side-store | The authoritative context every step reads |
| Gate-test | The concrete pass/reject question |
| Done-criterion | Fits + means-what-intended + verified clean |
| Verify harness | How you watch the built thing behave |

See [`METHODOLOGY.md`](./METHODOLOGY.md) for a worked example (filling the slots for a web service).

## License

[MIT](./LICENSE) — use it, fork it, adapt it, ship it.

## Contributing

Issues and PRs welcome. The methodology is meant to be adapted; if you find a sharper framing or a missing discipline, open a discussion.
