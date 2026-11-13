# NetEase Cloud Music API add-on

This add-on wraps the official multi-architecture Docker image of
[NeteaseCloudMusicApiEnhanced](https://github.com/NeteaseCloudMusicApiEnhanced/api-enhanced)
for use with Music Assistant.

- Upstream release: **4.41.1** (pinned)
- Container port: `3000`
- Host port: `3000` by default
- No persistent data: anonymous token and keys live in `/tmp` and are rebuilt on start

## Why a wrapper

The upstream project already publishes a clean Node.js Docker image. This
repository only adds the Home Assistant add-on metadata, so there is no
business logic fork to maintain. Updating is a two-line change:

1. `config.yaml`: bump `version`
2. `Dockerfile`: bump `ARG UPSTREAM_IMAGE`

## Install

1. Add this repository to Home Assistant:
   **Settings → Add-ons → Add-on store → ⋮ → Repositories**
   URL: `https://github.com/Square-N/netease-api-addon`
2. Install **NetEase Cloud Music API**.
3. Start it.
4. Verify:
   ```bash
   curl http://<HA_HOST>:3000/inner/version
   ```
   Expected: `{"code":200,"data":{"version":"4.41.1"}}`

## Music Assistant

In Music Assistant, set the NetEase provider **API base URL** to:

```text
http://<HA_HOST>:3000
```

If you temporarily map the host port to `3001` while testing, use `3001`
instead.

## Port conflict

If the old NetEase API add-on is still running on port `3000`, either:

- stop the old add-on first, or
- change this add-on's host port to `3001` in the add-on **Network** tab,
  test it, then switch it back to `3000` after stopping the old add-on.

## Update policy

This repository pins an upstream **release tag**, not `latest`. Bump the
version deliberately after checking the upstream release notes. Do not use
`latest`: Home Assistant uses the add-on `version` for update detection,
and a moving tag makes rollback and bug reports ambiguous.
