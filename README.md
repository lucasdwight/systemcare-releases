# iSharpe SystemCare — releases

This repository exists so that installed copies of **iSharpe SystemCare** can find out when a
newer version has been published. It holds no source code.

| File | What it is |
|---|---|
| `latest.json` | The newest published version, where its installer lives, and that installer's SHA-256. |
| `latest.json.sig` | A detached signature over `latest.json`, made with the product's release key. |

Installers are attached to the [Releases](../../releases) of this repository.

## Why the signature matters

An installed copy will not act on `latest.json` unless the signature verifies against a public
key compiled into it. That is the only thing it trusts — not this repository, not GitHub, not
HTTPS. A manifest served from anywhere else, or edited after signing, is refused and nothing is
downloaded.

So `latest.json` must never be edited in place, reformatted, or re-saved by a tool that might
change its whitespace or line endings. A single altered byte invalidates the signature, and
every installation will correctly stop updating until a properly signed manifest is published.

To publish a new version, build the installer and run `tools/sign-release.ps1` in the main
repository, then replace both files here and attach the new installer to a release.
