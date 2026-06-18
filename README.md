# homebrew-tap

A [Homebrew](https://brew.sh) tap for lightning-rider-999's command-line tools.
It serves prebuilt, checksummed release binaries as Homebrew **casks**, so
macOS and Linux users can install the CLIs without a Go toolchain.

## Install

Tap-qualified — no `brew tap` step needed:

```sh
brew install lightning-rider-999/tap/stashbox
brew install lightning-rider-999/tap/stash
```

Or tap once, then install by the short name:

```sh
brew tap lightning-rider-999/tap
brew install stashbox
brew install stash
```

Upgrade and uninstall as usual:

```sh
brew upgrade stashbox stash
brew uninstall stashbox stash
```

## What's in the tap

| Cask       | Command after install | Tool                                                                       | Source repo                            |
|------------|-----------------------|----------------------------------------------------------------------------|----------------------------------------|
| `stashbox` | `stashbox`            | **Read-only** client/CLI for a [stash-box](https://github.com/stashapp/stash-box) GraphQL instance (StashDB or any other). | [`lightning-rider-999/go-stashbox`](https://github.com/lightning-rider-999/go-stashbox) |
| `stash`    | `stash`               | Query **and** operate a self-hosted [Stash](https://github.com/stashapp/stash) media server over its GraphQL API. | [`lightning-rider-999/go-stash`](https://github.com/lightning-rider-999/go-stash) |

The casks wrap the prebuilt release archive for your OS/arch rather than
building from source. On macOS the install hook strips the `com.apple.quarantine`
xattr so Gatekeeper doesn't block the unsigned binary on first run.

## How the tap is maintained

The cask definitions under `Casks/` are **generated and pushed by each tool's
release automation** ([GoReleaser](https://goreleaser.com)) when a new version
is tagged — do not hand-edit them. Each release stamps the new version, archive
URLs, and sha256 checksums into the cask. A tap with no releases yet simply has
no casks; they appear with the first tagged release of each tool.

## Other ways to install these tools

Homebrew is one option. Both CLIs also install via `go install`, a checksum-
verifying `install.sh`, or a manual archive download — see each tool's own
README:

- [`go-stashbox`](https://github.com/lightning-rider-999/go-stashbox) — the `stashbox` read-only stash-box client/CLI.
- [`go-stash`](https://github.com/lightning-rider-999/go-stash) — the `stash` Stash-server client/CLI.

## Driving these tools from Claude Code

Both CLIs are agent-first. The
[`lightning-rider-999/lightning-rider-plugins`](https://github.com/lightning-rider-999/lightning-rider-plugins)
marketplace ships thin, skill-only Claude Code plugins (`stashbox`, `stash`)
that drive these binaries — each plugin checks the binary is installed (Homebrew
being one supported path) and discovers its live operation surface from the
binary itself.

## Related repositories

This tap is the install channel for a small family of related repos:

- [`go-stashbox`](https://github.com/lightning-rider-999/go-stashbox) — source for the `stashbox` cask: a read-only Go client/library & CLI for any stash-box GraphQL instance.
- [`go-stash`](https://github.com/lightning-rider-999/go-stash) — source for the `stash` cask: a Go client/library & CLI for a self-hosted Stash media server.
- [`lightning-rider-plugins`](https://github.com/lightning-rider-999/lightning-rider-plugins) — Claude Code plugin marketplace that drives the installed `stashbox` and `stash` binaries.
- [`homebrew-tap`](https://github.com/lightning-rider-999/homebrew-tap) — this repo.
