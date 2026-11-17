# gripora-artifacts

Mirrors built binaries from the other Gripora repositories as plain
git-tracked files, so a browser can fetch them.

## Why this repo exists

GitHub release assets are served from `release-assets.githubusercontent.com`,
which sends no `Access-Control-Allow-Origin` header, so an in-browser
`fetch()` of a release asset is blocked by CORS. Files committed to a public
repo don't have this problem: `raw.githubusercontent.com` and
[jsDelivr](https://www.jsdelivr.com/) serve them with permissive CORS headers.

So the producing repo's CI commits each build here as well, and the web
Configurator's firmware flasher (cfg.gripora.org) downloads it from here,
through `https://cdn.jsdelivr.net/gh/gripora-project/gripora-artifacts@master/`.

## Layout

```
firmware/<tag>/<filename>
```

`<tag>` is the exact git tag of `gripora-firmware` that produced the build,
for example `snapshot/0.0.1` or `release/1.0.0`. Nothing is ever overwritten.

## Who writes here

The firmware's `snapshot.yml`, `release.yml` and `dev-build.yml` workflows,
through a GitHub App with Contents read/write on this repository only. Its
id and private key are the secrets `ARTIFACTS_APP_ID` and
`ARTIFACTS_APP_PRIVATE_KEY` on `gripora-firmware`.
