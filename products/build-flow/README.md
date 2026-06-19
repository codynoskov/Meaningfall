# Build Flow

Build Flow is the guided product-composition product under the Meaningfall umbrella. It runs staged creation and review flows that compose product artifacts over time.

Current package: **v0.2.0**.

Build Flow is intentionally narrow right now: it has **one stage**, Product Brief, and Product Brief creates or updates the starter product-memory surface around `PRODUCT.md`. Additional stages are deferred until there is concrete pressure for them — Build Flow does not promise DesignMD, component generation, visual reference generation, stack analysis, prototype generation, or test-data planning today.

## Boundaries

- Build Flow owns **stage orchestration**: which stages exist, what each stage may create or update, guided interview behavior, handoff, and how the Seed Loop discipline is instantiated for a stage.
- It does **not** define the `PRODUCT.md` format. The format is owned by ProductMD; its single source of truth is the ProductMD spec. If a stage reveals missing product meaning, that reusable change belongs in ProductMD, not inside a Build Flow stage.
- It does **not** own the future Memory package. Product Brief installs the current accepted starter surface for product memory, but `products/memory/` remains deferred until Memory has concrete public tooling, documentation, or client pressure.
- It does **not** redefine the build-and-verify discipline. Build Flow instantiates [Seed Loop](../seed-loop/README.md) for a stage; the discipline itself stays domain-neutral.
- Product Brief verification checks are stage-local and derived from the ProductMD spec. They are not a second normative ProductMD format authority.

## Stages

| Stage | Role | Output |
| --- | --- | --- |
| Product Brief | Interview from a rough idea, notes, or a scoped update request. | Creates or updates the starter product-memory surface: `PRODUCT.md`, `product-memory/README.md`, create-on-need supporting files, and default-on approval-visible `AGENTS.md` integration. |

The Product Brief stage is packaged as an Agent Skill (the open `SKILL.md` standard) at [`skills/product-brief/`](skills/product-brief/). It instantiates the Seed Loop over ProductMD's owners and references the ProductMD spec by URL — it does not restate the format.

## Product Memory Install

For a new product, Product Brief installs the current accepted product-memory starter surface:

```text
PRODUCT.md
product-memory/
  README.md
  notes.md       # create-on-need
  decisions.md   # create-on-need
  drafts.md      # create-on-need
  glossary.md    # create-on-need
  archive/       # lazy, first supersession
AGENTS.md        # default-on approval-visible integration; host-owned
```

Only `PRODUCT.md` and `product-memory/README.md` are structural product-memory files that are always created for a new install. Supporting files are created only when Product Brief has content for them. `AGENTS.md` is recommended by default for AI-assisted work, but remains host-owned and the user may opt out.

The operational install contract is [`skills/product-brief/references/product-memory-install.md`](skills/product-brief/references/product-memory-install.md). ProductMD format verification remains in [`skills/product-brief/references/verification.md`](skills/product-brief/references/verification.md).

## Run the Product Brief stage

### In an AI IDE or agent — full mode

Install the skill in a skill-aware tool (Claude Code, Codex, Cursor, Gemini, and others), or upload it to claude.ai via Settings → Features. Point your tool at:

```text
skills/product-brief/
```

Then ask it to create product memory for a new product or to update an existing `PRODUCT.md`. The skill loads its reference material (the ProductMD spec, examples, verification reference, and install contract) only when needed.

### In an ordinary chat — lite mode

Use a chat that can read GitHub, and paste:

```text
Read and follow this skill, then run product-brief to help me create product memory for a new product:

https://github.com/codynoskov/Meaningfall/blob/main/products/build-flow/skills/product-brief/SKILL.md

Run the interview in English.
```

Change `English` to interview in another language. If the chat cannot open links, paste the contents of `SKILL.md` instead.

## Read

- [`skills/product-brief/`](skills/product-brief/) — the Product Brief stage (interview + Seed Loop instantiation for ProductMD and product-memory install).
- [`skills/product-brief/references/product-memory-install.md`](skills/product-brief/references/product-memory-install.md) — the Product Brief install contract.
- [ProductMD](../product-md/README.md) — the `PRODUCT.md` format this stage produces.
- [Seed Loop](../seed-loop/README.md) — the neutral build-and-verify discipline a stage instantiates.
- [`CHANGELOG.md`](CHANGELOG.md) · [`NOTICE`](NOTICE) · root [`LICENSE`](../../LICENSE)

## Older Meaningfall Brief Work

Build Flow Product Brief creates or updates product memory around `PRODUCT.md`. Older Meaningfall lab/reference brief work targeted Project Model source instead; it is not the public creation path in this package.
