# GitHub repository page metadata

Use these values when setting each repository's **About** panel. Keep the same organization and presentation across all
three repositories. Do not add the whole project to a fourth repository.

## `fundgraph`

**Description**

> Evidence-first dependency funding analysis, with clear provenance and uncertainty.

**Topics**

`open-source` `oss-sustainability` `dependency-analysis` `funding` `evidence` `typescript`

**Role**

Project source of truth: roadmap, product definition, security/contribution policy, release coordination, and cross-repo
documentation.

## `fundgraph-core`

**Description**

> TypeScript library for dependency discovery, funding evidence, relationship resolution, and deterministic reports.

**Topics**

`typescript` `dependency-graph` `open-source` `funding` `evidence` `library`

**Role**

Reusable library and domain logic. The `@fundgraph/core` package is prepared locally and has not been published.

## `fundgraph-cli`

**Description**

> Local-first CLI for dependency discovery and deterministic text or JSON reports.

**Topics**

`cli` `typescript` `dependency-analysis` `open-source` `developer-tools` `local-first`

**Role**

The `fundgraph` executable. It depends on the independently versioned `@fundgraph/core` package.

## Repository page presentation

- Use each repository's README SVG banner from its `assets/` directory.
- Keep descriptions short and state the distinct role of each repository.
- Add the repository's license, contribution, and security files through GitHub's recognized repository features.
- Pin `fundgraph` as the project overview, followed by `fundgraph-core` and `fundgraph-cli` on the organization profile.
- The README banners are SVGs. GitHub's social preview image is a separate repository setting and accepts raster image
  formats; create/upload those in GitHub only if you want a link-preview card in addition to the README banners.
