# eshobe-ecommerce-wp-theme-dist

Public build artifacts for the [Eshobe Ecommerce WP Theme](https://github.com/hamidnoshady/eshobe-ecommerce-wp-theme). No source code lives here.

WordPress reads this repo directly: `inc/theme-updater.php` fetches

```
https://raw.githubusercontent.com/hamidnoshady/eshobe-ecommerce-wp-theme-dist/main/<channel>/update.json
```

where `<channel>` is `stable` or `beta` (Technical Settings → “به‌روزرسانی قالب”).

## Layout

```
main/
  stable/
    update.json
    eshobe-ecommerce-wp-theme-<version>.zip
  beta/
    update.json
    eshobe-ecommerce-wp-theme-<version>.zip
```

`update.json` shape:

```json
{
  "version": "0.8.26",
  "download_url": "https://raw.githubusercontent.com/hamidnoshady/eshobe-ecommerce-wp-theme-dist/main/stable/eshobe-ecommerce-wp-theme-0.8.26.zip",
  "published_at": "2026-11-19T17:20:00Z",
  "sha256": "...",
  "changelog": "..."
}
```

- `version` must match `x.y.z` and be greater than the installed theme version.
- `download_url` **must** point inside this repo (raw file or this repo's releases); anything else is rejected by the updater.
- `sha256` is verified before WordPress installs the zip.
- `beta` mirrors `stable` until a separate beta pipeline exists.

## Who writes here

The Release workflow in the source repo commits the zip and both manifests on every version-bumping merge to `main`. It needs the `DIST_REPO_TOKEN` secret (fine-grained PAT, `Contents: read and write` on this repo) in that repository.
