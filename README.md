# WindowIsReady_Remover — GNOME 51 fork

> **This is an unofficial fork.** The extension was created and is maintained by
> **[Nuno Farruca](https://github.com/nunofarruca)** and contributors —
> original repository: **[nunofarruca/WindowIsReady_Remover](https://github.com/nunofarruca/WindowIsReady_Remover)**,
> published on [extensions.gnome.org](https://extensions.gnome.org/extension/1007/window-is-ready-notification-remover).
>
> This fork only adds GNOME 51 support while waiting for an upstream release.
> It is **not published on extensions.gnome.org** — it is meant for local installation only.
> The change has been offered upstream as a pull request. Once the original
> extension supports GNOME 51, please use it instead of this fork.

## What the extension does

Removes the "*Window* is ready" notification in the GNOME desktop
environment by disconnecting the shell's listener for it, so the message never appears.

## Changes in this fork

| | Upstream | This fork |
|---|---|---|
| Supported GNOME Shell versions | 45–50 | 45–51 |
| How the notification is suppressed | Blocks the *first* handler found for the `window-demands-attention` / `window-marked-urgent` signals | Disconnects only the handlers owned by GNOME Shell's `Main.windowAttentionHandler`, and reconnects them on disable |

The second change matters because the first handler found for those signals
can belong to a dock (e.g. Dash to Dock) or another extension rather than to
the shell, in which case the notification still shows.

All changes are in [one commit](../../commits/gnome-51) on top of upstream
`master`; the full upstream history is preserved.

Tested on GNOME 51.

## Installation (local)

```bash
git clone -b gnome-51 https://github.com/olexandrtkachenko/WindowIsReady_Remover.git
cd WindowIsReady_Remover
cd windowIsReady_Remover@nunofarruca@gmail.com
zip -r ../windowIsReady_Remover.zip metadata.json extension.js
gnome-extensions install --force ../windowIsReady_Remover.zip
```

Log out and back in (required on Wayland), then:

```bash
gnome-extensions enable windowIsReady_Remover@nunofarruca@gmail.com
```

The fork keeps the original UUID on purpose: it replaces the upstream
extension in place, and you can switch back to the official version from
extensions.gnome.org at any time.

## License

Apache License 2.0, as declared by the original author in `metadata.json`.
Copyright belongs to the original author and contributors; modifications in
this fork are marked in the changed files and listed above.
