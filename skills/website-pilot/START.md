# Start a Meaningfall Website Pilot

## Share this prompt

```text
Read and follow the current official Meaningfall Website Pilot bootstrap:
https://github.com/codynoskov/Meaningfall/blob/main/skills/website-pilot/START.md

Start or continue a Meaningfall Website Pilot Project in this current repository.

If this repository is the Meaningfall distribution/source repository rather than the
website Project repository, ask me for the target repository before changing Project files.
```

This is the short client-facing entry prompt. It works whether Meaningfall is
absent, already installed, old, partial, or duplicated. It deliberately points to
this live bootstrap route; the installed package is versioned and release-pinned.

## Bootstrap and release source

The current compatible package is the latest official release asset:

`https://github.com/codynoskov/Meaningfall/releases/latest/download/meaningfall-website-pilot.zip`

For a repeatable installation, use the version-specific asset URL from the release
page and record its SHA-256. Download the asset into a temporary directory, unpack
it, and run the bundled `scripts/website_pilot.py lifecycle` command against the
chosen Codex skills root. It delegates install, reuse, update, repair, and
readiness checks to the bundled lifecycle owner. Do not hand-copy files or create a
second installed Skill directory.

The package prints material technical-feedback events. `READY` means the release,
profile, managed file receipt, and safe diagnostic passed. Codex discovery and
actual invocation remain separate: if Codex does not show the Skill after the
normal client refresh/restart path, report that as `LIMITED` rather than claiming
success. Once callable, select the `website-pilot` profile and continue directly
to safe Project creation or resumption.

## Project repository boundary

The current repository is normally the Website Project repository: create or resume
the pilot there. Do not create a second repository merely because the Project is new.
If the current repository is Meaningfall's distribution/source repository, pause for
one concrete target-repository question before changing Project files. If a current
repository is nonempty but is neither a valid Website Project nor the selected
Project repository, preserve its files and ask that same concrete question.

## Capability boundary

The minimum route needs the selected Project repository, filesystem access, Git, Python,
and a local browser or Codex preview surface. Node/npm and a website framework are
selected only when the accepted Realization needs them. Do not install a CMS,
analytics, or a provider merely because it exists.

- **DataForSEO:** use only when Website Guidance finds that search evidence could
  materially change positioning, information architecture, terminology, or Product
  Meaning. On macOS, use the project owner's existing Keychain route only after the
  applicable service/account is identified and access is authorized. Never put a
  secret in chat, repository files, technical trace, command history, or a browser
  URL. Missing access is `USER_ACTION_REQUIRED`, not a reason to invent research.
- **Mobbin:** use only when visual/reference research is relevant. Detect the MCP
  connection first; connect it through the owner's supported MCP setup when absent.
  Its absence does not block independent Product, Content, or local Realization work.
- **Cloudflare:** activate only after local preview and browser verification pass and
  the owner explicitly authorizes the production publication effect. Detect the
  authorized connection then; do not make an account, deploy, or expose localhost
  before that point.

The package's Project trace records capability state and verification evidence, not
credentials or a second configuration/task authority. It creates no Actor state.

## What this route verifies

The released synthetic fixture exercises installation recovery, an Actor-free
Project, candidate/accepted Product Meaning, localhost-only preview, rendered
route verification, correction/rebuild, and continuation from Project-local state.
It does not claim production publication, an active DataForSEO account, an active
Mobbin connection, an active Cloudflare connection, or a client invocation that was
not actually observed.
