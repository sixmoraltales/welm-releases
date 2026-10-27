# welm releases

Release binaries and the Sparkle appcast for **welm**, a macOS app that plays contextual
ambient soundscapes based on the app you're using.

This repository holds no source code. It exists because Sparkle fetches its feed over
unauthenticated HTTPS, which a private repository's release assets can't serve.

## Layout

Every build and the appcast live on a single long-lived release tagged
[`releases`](../../releases/tag/releases), rather than one tag per version. This keeps the feed
URL and the download prefix constant forever:

```
appcast   https://github.com/sixmoraltales/welm-releases/releases/download/releases/appcast.xml
prefix    https://github.com/sixmoraltales/welm-releases/releases/download/releases/
```

A tag per version does not work here: `generate_appcast` stamps every item in the feed with a
single URL prefix, so older items would point at the newest tag and 404.

## Installing

Download the latest `welm-<version>.zip` from the
[`releases`](../../releases/tag/releases) assets, unzip, and drag `welm.app` to
`/Applications`. The app updates itself from then on.

Builds are Developer ID signed and notarized by Apple.

## Internal channel

Internal test builds ("welm Internal", a separate app that installs beside welm and talks to
the development backend) live on a second long-lived release tagged
[`internal`](../../releases/tag/internal), with its own appcast:

```
appcast   https://github.com/sixmoraltales/welm-releases/releases/download/internal/appcast.xml
prefix    https://github.com/sixmoraltales/welm-releases/releases/download/internal/
```

They are not for general use: they point at a test backend and carry features that are not
in the public app.
