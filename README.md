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
| `pull-request` | PR targeting any branch | Cache pull, xcode-test, xcodebuild, cache push |
| `release` | Manual | Cache pull, xcode-archive (App Store), build summary |
| `hello-world` | Manual | Echo "Hello World" |

## Trigger Map

Builds are triggered automatically via the `trigger_map` in the pipeline YAML:

```yaml
trigger_map:
  - push_branch: main
    workflow: primary
  - pull_request_target_branch: "*"
    workflow: pull-request
```

- **Push to `main`** → runs the `primary` workflow (archive + test)
- **Pull request targeting any branch** → runs the `pull-request` workflow (test + build)
- **`release` and `hello-world`** are manual-only (run from the dashboard or CLI)

## Setup

This project was initialized with:

```bash
ci init --create
```

This generated both the pipeline YAML and the GitHub Actions workflow automatically.
