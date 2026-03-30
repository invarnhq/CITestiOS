# CITestiOS

[![CI](https://github.com/invarnhq/CITestiOS/actions/workflows/ci.yml/badge.svg)](https://github.com/invarnhq/CITestiOS/actions/workflows/ci.yml)

Example iOS project with CI/CD powered by [cibuild](https://github.com/invarnhq/cibuild).

## What this demonstrates

- Zero-config CI setup with `ci init --create`
- Auto-generated GitHub Actions workflow using [`invarnhq/cibuild@v1`](https://github.com/invarnhq/cibuild)
- Xcode archive, test, and build steps running on GitHub Actions runners
- Separate workflows for push (`primary`), pull requests (`pull-request`), and tagged releases (`release`)

## Pipeline

The pipeline at [`.ci/pipelines/cibuild.yml`](.ci/pipelines/cibuild.yml) defines four workflows:

| Workflow | Trigger | Steps |
|---|---|---|
| `primary` | Push to `main` | Cache pull, xcode-archive, xcode-test, cache push |
| `pull-request` | Pull request | Cache pull, xcode-test, xcodebuild, cache push |
| `release` | Tag `v*` | Cache pull, xcode-archive (App Store), build summary |

## Setup

This project was initialized with:

```bash
ci init --create
```

This generated both the pipeline YAML and the GitHub Actions workflow automatically.
