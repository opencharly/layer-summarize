# AGENTS.md — layer-summarize

Standalone candy repo for the `summarize` layer — the `@steipete/summarize` CLI
installed globally via npm. The candy lives in `charly.yml` at the repo root: the
`require:` on `layer-nodejs`, the `check:` probes, and the embedded `skill:`
entity projected into the marketplace corpus as `/charly-tools:summarize`. The
npm package is pinned in `package.json`.

Canonical files:

- `charly.yml` — the `summarize:` candy entity and the `summarize-skill:` skill
  entity.
- `package.json` — pins `@steipete/summarize` for the global npm install.
- `.github/workflows/tag-on-merge.yml` — CalVer tag + `CHANGELOG/` on merge.
- `README.md` — user overview only; never agent guidance.

## Load these skills first (R0)

- `/charly-tools:summarize` — the owning skill. The npm-global install path, the
  `summarize`/`summarizer` binaries, and the URL/file extraction surface. Load
  before editing or troubleshooting the candy.
- `/charly-image:layer` — the candy authoring reference (`charly.yml` schema,
  `plan:` step verbs incl. `check:`, package sections). Load before editing any
  entity field or plan step.

## Build / validate / test

- The merge gate is the **org-wide** `charly/pr-validator` (required check
  `validate / validate`, defined in `opencharly/.github`); this repo has **no
  per-repo candy gate** and ships only `.github/workflows/tag-on-merge.yml`.
- `charly box validate` at the repo root checks the manifest parses and
  validates.
- The candy's `plan:` `check:` steps are the functional evidence: the
  `summarize` and `summarizer` binaries, the unpacked scoped package, and
  `summarize --version` printing a version with a clean exit.

## Modify this repo

- Edit the `summarize:` candy entity AND the `summarize-skill:` skill entity in
  `charly.yml` together. The skill is the projected usage source, so a package or
  path change not mirrored in the skill leaves the corpus stale.
- Keep the npm package pin in `package.json` aligned with the skill and the
  `check:` probes.
- New behaviour claims belong in the `plan:` as an observable `check:` step, and
  in the skill body.

## Landing

- PR-only. Every change lands through a pull request; the org-required
  `charly/pr-validator` validates the diff and body and arms native auto-merge
  on PASS. Direct pushes to `main` are blocked.
- History lives in `CHANGELOG/` (written by `tag-on-merge` at merge time); the
  PR body IS the changelog.
- The authoritative rulebook is the umbrella `AGENTS.md` in
  `opencharly/opencharly` and `charly/AGENTS.md` in the charly repo. Do not
  restate its rules here.
