# kb-assets-mirror

Static asset mirror for internal desktop tooling.

Files here are produced by an automated publish pipeline. Editing them by hand
will simply be overwritten on the next publish — please don't.

## Layout

| file | purpose |
| --- | --- |
| `manifest.json` | index of the current asset: version, size, checksum, signature pointer |
| `manifest.sig`  | detached signature over the exact bytes of `manifest.json` |
| `bundle.bin`    | the asset bundle itself (opaque; consumed as a single blob) |

## Consumer contract

Clients **must** verify `manifest.sig` against their pinned public key *before*
trusting anything inside `manifest.json`, and must verify the downloaded bundle
against the checksum declared there. A signature mismatch is a hard failure —
clients are expected to refuse the update rather than fall back to the bundle.
