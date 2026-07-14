# esqLABS R-universe

This repository is the **R-universe registry** for the esqLABS R packages. It is not an R package itself; its only job is to hold `packages.json`, the list of package repositories that [R-universe](https://r-universe.dev) builds and publishes to https://esqlabs.r-universe.dev.

## Installing from this universe

Users can install ESQlabs packages with plain `install.packages()`:

```r
install.packages(
  "esqlabsR",
  repos = c(
    esqLABS = "https://esqlabs.r-universe.dev",
    OSP = "https://open-systems-pharmacology.r-universe.dev",
    CRAN = "https://cloud.r-project.org"
  )
)
```
## What gets built

`packages.json` lists the public esqLABS R packages that publish GitHub releases. Each entry tracks the package's latest release (`"branch": "*release"`).

| Package | Source repository |
| --- | --- |
| `esqlabsR` | `esqLABS/esqlabsR` |
| `osp.snapshots` | `esqLABS/osp.snapshots` |

Other esqLABS R packages were deliberately left out for now:

- Packages with **no GitHub release** cannot be tracked with `*release` (R-universe has nothing to resolve). Give a package a release, then add it here.
- **Private** repositories will not build on a public universe.
- Shiny-app packages and unfinished package skeletons are not distributed as library dependencies.

## Maintaining the list

- **Add a package**: append an object with its `package` name (the `Package:` field from the repository's `DESCRIPTION`) and its `url`. If the package does not cut GitHub releases, drop the `"branch"` field so R-universe builds its default branch instead of `*release`. **Also grant the R-universe GitHub App access to the new package's repository**: the app is installed on the `esqLABS` org with "only select repositories" scope, so each newly listed package repo must be added to its allow-list (Org settings -> GitHub Apps -> r-universe -> Configure). A public repo is read anyway, but adding it explicitly is the reliable path; a private repo will not build on a public universe.
- **Remove a package**: delete its object.
- **Change what is tracked**: edit or remove the `"branch"` field on that package's entry.

Every push to this repository triggers R-universe to re-read `packages.json` and reconcile what it builds. `packages.json` is validated as strict JSON; keep it well-formed (no comments, no trailing commas).
