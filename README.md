# scriptor-papers-out

Generated public paper outputs for the scriptor research workflow. In this
monorepo, this GitHub-hosted folder is the canonical output root; Dropbox or
other sync folders can mirror it, but they are not the source of truth.

This repository is intended to be pushed to GitHub and served with GitHub Pages
from the `docs/` directory.

Generated structure:

```text
papers/<paper-id>/latest/
pdfs/
corpus/paper_status.json
corpus/self_improvement_report.md
```

The committed output root only keeps `latest/` bundles. Timestamped `runs/`
snapshots are available for local audit work, but are git-ignored so dynamic
publishing does not create noisy history.

`pdfs/` is intentionally plain: it contains only the latest PDF for each
registered paper, using title-slugged filenames.

`corpus/self_improvement_report.md` is generated on every local publish. It asks
subject-aware reviewer and methods questions so the next run can improve the
paper and the pipeline itself.

GitHub Pages serves a mirror of the latest bundles from:

```text
docs/papers-out/
```

Do not edit generated paper bundles by hand. Change the source paper ledger or
`scriptor-meta`, then rebuild.
