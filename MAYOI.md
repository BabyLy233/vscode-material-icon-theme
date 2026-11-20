# Mayoi packaging

This fork keeps a Mayoi plugin built from upstream's icons. `main` follows
[material-extensions/vscode-material-icon-theme](https://github.com/material-extensions/vscode-material-icon-theme);
the **Build Mayoi plugin** workflow builds the latest upstream release and force-pushes the result to the `mayoi`
branch.

Upstream releases about every three or four weeks (median 25-28 days), so the workflow checks weekly, on Monday, and
skips the build when `mayoi` already has that version. A manual **Run workflow** always rebuilds, which is useful after
a change to the workflow itself.

Install it with:

```sh
mayoi plugin install BabyLy233/vscode-material-icon-theme@mayoi
```

Then choose **View → Theme → File Icon Theme… → Material Icon Theme**.

## The branches

- `main` is upstream's code, plus `.github/workflows/mayoi.yml` and this note. Use **Sync fork** as usual.
- `mayoi` is generated: `plugin.json`, `dist/material-icons.json`, `icons/`, `LICENSE` and a README. Do not edit it by
  hand; the daily workflow (and **Run workflow**) rewrites it.

## Build it locally

```sh
npm ci --ignore-scripts --no-audit --no-fund
mkdir -p dist
npm run generateJson > dist/material-icons.json
npm run generateOpenFolders
npm run generateClones
```

The three scripts generate the default file and folder icons, the open folder variants and the icon clones that the
manifest names. Copy `dist/`, `icons/` and `LICENSE` beside a `plugin.json` like the one the workflow writes.

The upstream extension build (`npm run build`) is for VS Code and is not needed for the Mayoi plugin.