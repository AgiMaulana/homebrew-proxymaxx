# ProxyMaxx Homebrew tap

Homebrew cask for [ProxyMaxx](https://github.com/AgiMaulana/ProxyMaxx) — a native macOS
HTTP/HTTPS debugging proxy.

## Install

```sh
brew tap AgiMaulana/proxymaxx
brew trust --tap agimaulana/proxymaxx
brew install --cask AgiMaulana/proxymaxx/proxymaxx
```

`brew trust` is needed once. Homebrew refuses to load a cask from a tap that is not in its
trust list, and this is not an official tap. See `brew help trust`.

## Upgrade and remove

```sh
brew upgrade --cask proxymaxx
brew uninstall --cask proxymaxx
brew uninstall --zap --cask proxymaxx   # also drops ~/Library/Application Support/ProxyMaxx
```

## Why this cask clears the quarantine attribute

ProxyMaxx is ad-hoc signed: no Apple Developer ID, no notarization. Homebrew quarantines every
cask it downloads, and macOS refuses to launch a quarantined app whose signature it cannot
verify, showing:

> Apple could not verify "ProxyMaxx" is free of malware that may harm your Mac or compromise
> your privacy.

So after installing the app, this cask runs:

```sh
xattr -dr com.apple.quarantine "/Applications/ProxyMaxx.app"
```

### Security notice

That step bypasses Gatekeeper for the installed app. Please install only if you trust
[the source](https://github.com/AgiMaulana/ProxyMaxx). If you would rather keep Gatekeeper in
the loop, take the DMG from
[the release](https://github.com/AgiMaulana/ProxyMaxx/releases/latest) instead and approve the
app by hand in **System Settings → Privacy & Security**.

### The honest fix

Notarizing the app with an Apple Developer ID would remove the need for the `postflight` above,
and would let the plain DMG install warning-free as well. Until then the cask does the `xattr`
step so users do not have to.

## Casks in this tap

| Cask | Description |
| --- | --- |
| `proxymaxx` | Native macOS HTTP/HTTPS debugging proxy |

`Casks/proxymaxx.rb` is generated. Do not edit it here: it is written on every `vX.Y.Z` tag by
[`.github/workflows/release.yml`](https://github.com/AgiMaulana/ProxyMaxx/blob/main/.github/workflows/release.yml)
from
[`Scripts/homebrew/proxymaxx.rb`](https://github.com/AgiMaulana/ProxyMaxx/blob/main/Scripts/homebrew/proxymaxx.rb).
