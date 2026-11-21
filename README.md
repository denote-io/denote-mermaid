# Mermaid diagrams

Render local Mermaid fenced blocks in Markdown rich view with strict source and SVG safety boundaries.

This is an optional [Denote](https://github.com/mbianchidev/denote) plugin. Its
user guide is [guide.md](guide.md); Denote shows the same guide in
**Settings → Plugins**.

## Install

Enable **Mermaid diagrams** from **Settings → Plugins** in Denote. Denote
downloads the release archive pinned in its built-in catalog, verifies its size
and SHA-256 digest, and only then loads the plugin in an isolated worker.

## Development

Use the Node.js version in `.node-version`.

```bash
npm ci
npm run typecheck
npm test
npm run check     # manifest, guide, and import boundaries
npm run package   # build, verify, and write .plugin-artifacts/denote.mermaid-<version>.tgz
```

`npm run dev` rebuilds `.plugin-dev/denote.mermaid.tgz` on every change. Load it
in Denote Development from **Settings → Plugins → Load local plugin archive**.
Disable the local plugin before loading rebuilt bytes with the same ID.

The build uses the [Denote plugin SDK](https://github.com/denote-io/denote-plugin-sdk)
and its `denote-plugin` command. It produces a single self-contained worker
bundle and a reproducible archive with fixed file modes, no timestamps, and LF
text. The pinned Vite and Rolldown versions keep archive bytes stable.

## Release

Published versions are immutable. To release a change:

1. Bump `version` in both `plugin.json` and `package.json`.
2. Merge to `main` with CI passing.
3. Run the **Release** workflow. It builds, verifies, and publishes
   `denote.mermaid-<version>.tgz` as the `v<version>` release asset.
4. Update the plugin's entry in Denote's catalog to the new release so the
   application offers it.

## History

This plugin was developed in `plugins/mermaid` of
[mbianchidev/denote](https://github.com/mbianchidev/denote), whose history for
this directory is preserved here. `releases.json` records every version
published from that repository, with its source commit there, original asset
URL, size, and SHA-256 digest.

[v0.3.0](https://github.com/denote-io/denote-mermaid/releases/tag/v0.3.0) republishes the identical archive Denote
already offers (`c1fcb78c9404c375a98b778c865417cac72863096d09fc49ae3d86574b71cf65`, 317860 bytes),
built from source commit `ee115d51b2b3dc4d941d5abfd16ed1e2c2054dbe` in
mbianchidev/denote. The source in this repository is unchanged from that commit.

That archive was built against the plugin SDK as of its source commit, which
predates SDK v0.1.0. Rebuilding with SDK v0.1.0 therefore produces different
bytes; the published archive stays authoritative. CI tolerates this for
v0.3.0 only, so every later version must rebuild byte for byte.

## License

[MIT](LICENSE)
