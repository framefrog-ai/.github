# framefrog-ai organization profile — setup

This repository is the special **`.github`** repository that renders the public
organization page at <https://github.com/framefrog-ai>. GitHub only shows
`profile/README.md`; the rest of the tree is supporting assets.

## 1. The repository must be named `.github` (owner, one-time)

GitHub renders the organization page **only** from a public repository whose
name is exactly `.github`, using its `profile/README.md`. It does not create
that repository from a push, and a repository named `github` will **not** render
the org page.

Current state: the tree is pushed to `framefrog-ai/github`
(<https://github.com/framefrog-ai/github>). Rename it once:

1. <https://github.com/framefrog-ai/github/settings> → **General**
2. **Repository name** → type `.github` → **Rename**
3. GitHub redirects the old URL, so the pushed history stays valid.

After the rename, verify:

```bash
curl -s -o /dev/null -w '%{http_code}\n' https://raw.githubusercontent.com/framefrog-ai/.github/main/profile/assets/banner.svg
```

→ `200` means the banner raw URL resolves and the org page can render it.

If a fresh repository is preferred instead:

1. <https://github.com/organizations/framefrog-ai/repositories/new>
2. Name: `.github` — visibility: **Public** — do **not** initialize with a README.
3. Then:

```bash
git remote add profile git@github.com:framefrog-ai/.github.git
git push -u profile main
```

## 2. Organization settings (owner, web UI)

These cannot be changed from git; set them in **Organization settings → Profile**:

| Field | Value |
|---|---|
| Display name | `FrameFrog` |
| Bio | `Serverless AI video post-production — NVDEC, SAM 2, 3D LUT, RIFE, Real-ESRGAN, NVENC on zero-copy CUDA. framefrog.me` |
| Website | `https://framefrog.me` |
| Email (public) | `contact@framefrog.me` |
| Location | optional |
| Avatar | upload `profile/assets/avatar.png` (1000×1000, charcoal + emerald aperture) — the same mark is also shown in the README, so the page reads correctly even before this step |
| Social preview | upload `assets/social-preview.png` (1280×640, rendered from the banner) under **Settings → Social preview** |
| README visibility | enabled automatically once `profile/README.md` is pushed to the `.github` repo |

Theme consistency is achieved through the README itself: GitHub has no custom
org theme, so all imagery and badges are pinned to `#0D1117` / `#10B981`, and the
README is designed to read cleanly on both GitHub dark and light modes.

## 3. Pin the public repositories

Pin, in this order:

1. `framefrog-pipeline` — the engine
2. `framefrog.github.io` — the product site

Add topics to both: `video`, `post-production`, `cuda`, `nvidia`, `sam2`,
`tensorrt`, `nvenc`, `agpl`.

## 4. Verify

- <https://github.com/framefrog-ai> shows the banner, badges, pipeline summary
  and links.
- The CI badge resolves to `framefrog-pipeline`'s workflow.
- The avatar matches the site's charcoal/emerald identity.
- `framefrog.me` header links back to the organization.
