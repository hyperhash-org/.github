# Hyper Hash – .github

This repository contains the **organisation-wide GitHub configuration** for the Hyper Hash Network project.

It defines all shared automation, templates, and community standards that apply across every Hyper Hash repository.

---

## Purpose

This repo provides:

1. **Reusable GitHub Actions workflows**
   - `rust-build.yml` — builds and tests Rust crates.
   - `docker-build.yml` — builds and pushes container images to GHCR.
   - `release.yml` — publishes tagged releases and attaches binaries.

2. **Community health files**
   - Issue templates for bug reports and feature requests.
   - Pull request template for consistent PR submissions.
   - CODEOWNERS to define default reviewers and maintainers.
   - CONTRIBUTING.md to outline contribution rules.
   - SECURITY.md for vulnerability reporting.
   - Optional Dependabot and Funding configuration.

3. **Organisation-wide defaults**
   - Shared labels, branch protection suggestions, and CI behaviour.
   - Ensures every repo (core, tp, pool, translator, ui, overlay, etc.) stays consistent.

---

## Using the reusable workflows

Each Hyper Hash repository can include very small workflow stubs that reference the reusable actions here.

Example for CI (Rust build):

# .github/workflows/ci.yml
name: ci
on: [push, pull_request]
jobs:
  build:
    uses: hyperhash-org/.github/.github/workflows/rust-build.yml@main
    with:
      run-tests: true
Example for Docker image build:

# .github/workflows/docker.yml
name: docker
on:
  push:
    branches: [ main ]
  push:
    tags: [ 'v*.*.*' ]
jobs:
  image:
    uses: hyperhash-org/.github/.github/workflows/docker-build.yml@main
    with:
      image-name: ${{ github.event.repository.name }}
Example for tagged release:

# .github/workflows/release.yml
name: release
on:
  push:
    tags: [ 'v*.*.*' ]
jobs:
  rel:
    uses: hyperhash-org/.github/.github/workflows/release.yml@main

Repository structure
pgsql
Copy code
.github/
  workflows/
    rust-build.yml
    docker-build.yml
    release.yml
  ISSUE_TEMPLATE/
    bug_report.yml
    feature_request.yml
  PULL_REQUEST_TEMPLATE.md
  CODEOWNERS
  CONTRIBUTING.md
  SECURITY.md
  dependabot.yml
  FUNDING.yml

Access and visibility
This repository is public so that reusable workflows can be referenced by all Hyper Hash projects and forks.
No secrets or credentials are stored here. All sensitive data (tokens, signing keys) are configured as organisation-level or repo-level GitHub secrets.

Maintainers
Hyper Hash Organisation
https://github.com/hyperhash-org

Primary Maintainer: Cal De Fenwycke (cal.defenwycke@gmail.com)

License
All workflow and template content in this repository is provided under the MIT License, so that anyone contributing to Hyper Hash or forking it can freely reuse the automation patterns.

---

Copyright (c) 2025 Hyper Hash Organisation
