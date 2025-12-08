# Release Runbook

Steps to create and publish a new release using the existing GitHub Actions scripts (run from repo root).

## Prerequisites
- Authenticated `gh` CLI with repo write access.
- `zip`, `bash`, and `git` available.
- Git tags fetched (so the latest tag is visible).
- `.genreleases/` will be recreated; ensure no important files are stored there.

## Steps
1) Compute next version (patch bump from latest tag):
```bash
GITHUB_OUTPUT=$(mktemp)
.github/workflows/scripts/get-next-version.sh
source "$GITHUB_OUTPUT"   # exports latest_tag and new_version
```

2) Abort if the release already exists:
```bash
GITHUB_OUTPUT=$(mktemp)
GITHUB_TOKEN=... .github/workflows/scripts/check-release-exists.sh "$new_version"
grep exists "$GITHUB_OUTPUT"   # expect exists=false
```

3) If `exists=true`, a release with that tag already exists (sometimes `get-next-version.sh` points at an already released tag if a newer release was created manually). Verify the most recent tags/releases with `git fetch --tags` and `gh release list`. 
   * bump the version yourself (e.g., pick the next patch number, set `new_version` manually, rerun step 2) before continuing.

4) Build release packages (creates `.genreleases/spec-kit-template-<agent>-<sh|ps>-<version>.zip`):
```bash
# Optional filters: AGENTS="claude qwen" or SCRIPTS=ps
.github/workflows/scripts/create-release-packages.sh "$new_version"
ls .genreleases/spec-kit-template-*-"$new_version".zip
```

5) Generate release notes from git history (writes `release_notes.md`):
```bash
.github/workflows/scripts/generate-release-notes.sh "$new_version" "$latest_tag"
```

6) Create the GitHub Release and upload artifacts:
```bash
GITHUB_TOKEN=... .github/workflows/scripts/create-github-release.sh "$new_version"
```

7) Optional: align `pyproject.toml` version in artifacts only:
```bash
.github/workflows/scripts/update-version.sh "$new_version"
```

Notes:
- Release title format: `Spec Kit Templates - <version-without-v>`.
- CI (`release.yml`) runs the same sequence on push to `main` (for specific paths) or via `workflow_dispatch`.
