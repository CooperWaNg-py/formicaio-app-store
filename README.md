# Formicaio Community App Store

umbrelOS community app store for [Formicaio](https://github.com/bochaco/formicaio),
which runs and manages nodes on the [Autonomi](https://autonomi.com) network.

The app is built from [CooperWaNg-py/formicaio](https://github.com/CooperWaNg-py/formicaio):
upstream Formicaio 0.8.8 plus fixes. Among them: nodes no longer fail with
`Exited (exit status: 2)` on every start or restart, which happens in the official
store's Formicaio 0.8.4, and new nodes now get the bootstrap peers they need to join
the network.

## Install

1. In umbrelOS, open the App Store, click the `⋯` menu at the top right, and choose
   **Community App Stores**.
2. Paste `https://github.com/CooperWaNg-py/formicaio-app-store` and click **Add**.
3. Open **Formicaio Community** and install **Formicaio**.

The app uses port 52102 and listens on the host only at the Docker gateway address,
on port 52104, so it can sit next to the official Formicaio app. Node P2P ports are
whatever you pick when you create nodes. Both apps would compete for those ports, so
run only one of them at a time.

To move existing nodes over from another Formicaio install, stop that app first. Its
data is not migrated automatically.

## Layout

| Path | Purpose |
| --- | --- |
| `umbrel-app-store.yml` | Store id (`formicaio-community`) and name |
| `formicaio-community-formicaio/` | The app. Its directory name must equal the app id, and the app id must start with the store id |
| `assets/` | Icon and gallery, referenced by absolute URL from `umbrel-app.yml` |

## Releasing a new version

1. In the Formicaio fork, run `gh workflow run umbrel_image.yml -f version=<version>`.
   The run summary prints `ghcr.io/cooperwang-py/formicaio:<version>-native@sha256:...`.
2. Paste that reference into `formicaio-community-formicaio/docker-compose.yml`.
3. In the same commit, set `version:` in `umbrel-app.yml` to `<version>` and update
   `releaseNotes`. umbrelOS offers an update only when `version` changes.
