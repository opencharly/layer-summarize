# summarize

The [summarize](https://www.npmjs.com/package/@steipete/summarize) CLI for
OpenCharly images — extracts text and transcripts from URLs and files.

The `summarize` candy installs `@steipete/summarize` globally via npm, so the
`summarize` binary (and its `summarizer` alias) are on `PATH`.

## What it provides

| Property | Value |
|---|---|
| Layer / candy | `summarize` |
| Binaries | `~/.npm-global/bin/summarize`, `~/.npm-global/bin/summarizer` |
| Package | `@steipete/summarize` (npm) |
| Requires | [`layer-nodejs`](https://github.com/opencharly/layer-nodejs) |
| Service / port | none |

## How to use it

Compose the layer by pinning this repo in a box's `candy:` list:

```yaml
my-agent-box:
  candy:
    base: fedora
    candy:
      - '@github.com/opencharly/layer-summarize:v2026.243.0410'
```

Then, inside the built image (or on a dev host):

```bash
summarize --version
summarize <url-or-file>
```

The candy's `plan:` asserts both binaries, the unpacked scoped package, and that
`summarize --version` prints a version and exits cleanly.

## Layout

- `charly.yml` — the `summarize:` candy entity (the `require:` on `layer-nodejs`
  and the `check:` probes) and the embedded `summarize-skill:` skill entity.
- `package.json` — pins `@steipete/summarize` for the global npm install.
- `.github/workflows/tag-on-merge.yml` — CalVer tag + `CHANGELOG/` on merge.
- `README.md` — this user overview.

## Related

- Owning skill: `/charly-tools:summarize`
- Dependency: `/charly-coder:nodejs`
- Bundle: `/charly-openclaw:openclaw-full`
- Speech-to-text companion: `/charly-tools:whisper`
- [`opencharly/charly`](https://github.com/opencharly/charly) — the charly CLI and image builder
- [`opencharly/opencharly`](https://github.com/opencharly/opencharly) — the umbrella
