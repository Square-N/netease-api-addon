# NetEase Cloud Music API — Home Assistant add-on repository

A minimal, pinned Home Assistant add-on wrapper for
[NeteaseCloudMusicApiEnhanced](https://github.com/NeteaseCloudMusicApiEnhanced/api-enhanced).

This repository contains no fork of the upstream API code. The add-on only
wraps the upstream multi-architecture Docker image, pinned to a release tag,
so Home Assistant can run the NetEase API inside the HAOS VM without an
external NAS/Docker host.

## Add this repository to Home Assistant

1. **Settings → Add-ons → Add-on store → ⋮ → Repositories**
2. Add:

   ```text
   https://github.com/Square-N/netease-api-addon
   ```

3. Install **NetEase Cloud Music API**.
4. Start it and verify:

   ```bash
   curl http://<HA_HOST>:3000/inner/version
   ```

   Expected version: `4.41.1`.

## Music Assistant

Point the Music Assistant NetEase provider **API base URL** at:

```text
http://<HA_HOST>:3000
```

If you map the add-on to host port `3001` for a side-by-side test, use
`3001` until you switch back to `3000`.

## Port conflict with the old add-on

The existing `NetEase Cloud Music API` add-on occupies port `3000`. Either:

- stop the old add-on before starting this one, or
- change this add-on's host port to `3001` in the add-on **Network** tab,
  test it, then switch to `3000` after stopping the old add-on.

## Update policy

- Upstream is pinned to **release tags**, never `latest`.
- To update, change exactly two version references:
  - `netease_cloud_music_api/config.yaml`: `version`
  - `netease_cloud_music_api/Dockerfile`: `ARG UPSTREAM_IMAGE` tag
- Then commit and push. Home Assistant will see the new add-on version.
- No automatic updater is configured, by design.

## Layout

```text
repository.yaml
netease_cloud_music_api/
├── config.yaml
├── Dockerfile
└── README.md
```

## License

The wrapper files in this repository are MIT licensed. The upstream
NeteaseCloudMusicApiEnhanced project is also MIT licensed.
