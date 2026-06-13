# Seed Loop

A neutral, domain-agnostic discipline for building a dependency-ordered artifact
and keeping it coherent. Version 0.1.0.

## Purpose

Many artifacts are made of parts that depend on each other in a definite order:
later parts rest on earlier ones. Such an artifact can be both *built* and *kept
consistent* by a single loop — grow it from its foundation outward, then verify
it back toward the foundation, repeating until nothing changes. The Seed Loop is
that loop, stated independently of what is being built.

It applies wherever there is a start that grounds everything, an end that is the
most derived, ordered parts between, and a notion of "this part is consistent
with what it depends on." A domain adopts the loop by supplying its own nodes and
its own notion of consistency (see Instantiating); the process is reused
unchanged.

## Nodes (the vocabulary)

- **node** — any element of the artifact; the general term.
- **seed** — the foundation everything else depends on. Usually a single start
  node; in a domain with cycles it may be a **foundational sub-graph** — the part
  that nothing depends back on.
- **joint** — an intermediate node on the path between seed and leaf.
- **leaf** — the end node: the most derived element.

Direction is **start → end**, not up/down — no spatial commitment. The loop is
**fractal**: a node's own internal structure may be a smaller seed loop, with its
own seed, joints, and leaf.

## The two passes

- **grow** — the authoring pass, start → end. Each node grows from its seed;
  earlier nodes are the ground for later ones.
- **root** — the verification pass, end → start. Root each node back to its
  seed. Where a node *will not root* — it needs something its seed does not yet
  provide, or it contradicts it — repair the **earlier** node it depends on
  (nearer the seed), not the current one.
- **settled** — the done state: a full grow/root pass that changes no node. The
  verification gate is passed.

The loop is **iterative to a fixpoint**, not a single pass: a repair during
`root` can require re-growing what depends on the repaired node, then rooting
again, until a pass is clean.

## Propagation (locality)

- A change invalidates only what is **downstream** of it — the nodes reachable
  from it along dependency edges.
- Re-traverse only the affected stretch. A full start→end pass is needed only
  when a change reaches the **seed** (or something every node depends on).
- Propagation follows **references (edges)**, not the nesting hierarchy.

## Correctness and priority

Two of these are properties of the loop; the third is a default a domain may set.

- **Invariant — a full `root` is always correct.** Re-rooting the whole artifact
  can never give a wrong result; it is only ever more work than strictly needed.
- **Invariant — locality is a description, not a cap.** The propagation rule says
  where a change *reaches*; it never forbids a wider pass.
- **Default (domain-overridable) — prefer quality.** When containment is not
  certain, take the full pass; quality wins ties; run a full `settled` pass
  periodically as hygiene against drift. A domain may override this trade-off —
  for instance, favor the cheap local pass under latency pressure or in
  throwaway work — but that override is a domain policy, not a change to the
  loop.

## Mechanism and oracle (the seam)

The loop separates two concerns so that its executor can change without changing
the discipline:

- **Mechanism (control)** — deterministic scheduling: which nodes to revisit, in
  what order, and when the artifact is `settled`. This is plain bookkeeping over
  the dependency graph and can be run by hand, by an agent, or by code.
- **Oracle (judgment)** — the single question "does this node root into its
  seed?" / "is this node consistent with what it depends on?" This is pluggable.
  It may be a human, an agent reading the artifact, or — for the parts that are
  formalizable — a deterministic checker.

The vocabulary above is the same whichever executor runs it. Swapping the
oracle, or moving the mechanism from soft execution to code, leaves the model
untouched.

### Properties that keep the loop executor-agnostic

- **Addressable nodes** — every node has a stable identity.
- **Addressed references** — a node names *what* it depends on, recoverably, so
  the dependency graph can be reconstructed (not "as above").
- **Guaranteed termination** — the loop must be unable to oscillate forever, so
  that `settled` is reachable. Termination holds in one of two regimes, by the
  shape of the dependency graph:
  - *Acyclic* — if dependencies form no cycles, `root` repairs upstream and
    terminates at the dependency-free seed; reaching the seed is the bound. An
    artifact acyclic by construction gets termination for free.
  - *Cyclic* — if nodes genuinely depend on each other in a loop, termination
    instead requires each repair to be **monotone** (it only tightens or adds,
    never undoes a prior repair), so the loop converges to a fixpoint — the way
    circular attribute grammars and chaotic iteration terminate. Monotonicity is
    straightforward to *engineer* for a **formalizable oracle** — define the
    repair over a lattice with monotone (inflationary) functions, as constraint
    propagation does — but it is not automatic even there: the functions must
    actually be monotone, not merely formalizable. For an **interpretive
    oracle** it is not free at all — a human or model can re-interpret
    non-monotonically and oscillate forever. There it must be
    **imposed as discipline**: allow repairs only to narrow or constrain, never
    to re-open; or **freeze the seed** (keep the foundation fixed and repair the
    cyclic cluster against it, which converts most of the work back to the
    acyclic regime).
  A deterministic executor relies on the same distinction: a topological rebuild
  for the acyclic case, a monotone fixpoint solver for the cyclic one.
- **Observe / mutate separation** — a check only reads; a repair writes. A check
  on a settled node is a no-op.

These cost nothing to adopt and are good hygiene on their own. Adopt the
properties; do not build machinery for an executor that does not exist yet.

## Instantiating the loop

A domain adopts the Seed Loop by supplying two things and reusing the rest:

1. **Its nodes and their order** — what the seed is, what the joints are, what
   the leaf is, and which node depends on which.
2. **Its oracle** — what "consistent" means in that domain.

The passes (`grow`, `root`), the `settled` gate, the propagation rule, and the
correctness invariants are reused unchanged.

---

## Lineage / relationship to prior work

Orientation, not implementation. The Seed Loop borrows posture and vocabulary
from established work; it does not claim to *be* any of these.

- **grow / root (two passes, start→end then end→start)** — attribute grammars:
  inherited attributes flow toward the leaves, synthesized attributes flow back
  toward the root; circular attribute grammars evaluate by fixpoint.
- **settled (fixpoint) and the priority on coherence** — fixpoint / chaotic
  iteration (the formal side); reflective equilibrium and the hermeneutic circle
  (the meaning side: mutual adjustment of foundation and particulars until they
  cohere).
- **propagation / locality** — incremental computation: dirty-propagation then
  demand-driven repair (Adapton), version-tracked query invalidation (Salsa).

If the mechanism is ever made deterministic code, take the control loop from this
incremental-computation line rather than reinventing it; keep the oracle
pluggable.
