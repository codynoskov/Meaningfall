# Seed Loop

A neutral, domain-agnostic discipline for building a dependency-ordered artifact
and keeping it coherent: grow it from its foundation outward, verify it back
toward the foundation, and repeat until nothing changes.

Current package: **v0.1.0**.

Seed Loop names the **process only**. It is independent of what is being built —
a domain adopts it by supplying its own nodes and its own notion of consistency,
and reuses the passes, the gate, and the propagation rule unchanged.

## At a glance

- **Nodes** — `seed` (the foundation everything depends on) → `joint`
  (intermediate) → `leaf` (the most derived). Direction is start → end.
- **Passes** — `grow` (author start → end) and `root` (verify end → start,
  repairing the earlier node when something will not root).
- **Gate** — `settled`: a full grow/root pass that changes no node.
- **Locality** — a change re-traverses only what depends on it; a full pass is
  needed only when the change reaches the seed.
- **Seam** — a deterministic *mechanism* (scheduling) over a pluggable *oracle*
  (the consistency judgment), so the same discipline runs by hand, by an agent,
  or as code.

## Adopt it

Supply two things; reuse the rest:

1. your **nodes and their order** — what the seed, joints, and leaf are, and which
   node depends on which;
2. your **oracle** — what "consistent" means in your domain.

The passes (`grow`, `root`), the `settled` gate, the propagation rule, and the
correctness invariants carry over unchanged.

## Read

- [`spec.md`](spec.md) — the full discipline (single source).
- [`CHANGELOG.md`](CHANGELOG.md) · [`NOTICE`](NOTICE) · root [`LICENSE`](../../LICENSE)

Seed Loop names no consumer; consumers reference it — it stays domain-agnostic.
(Who uses it is listed in the products index, not on this neutral surface.)
