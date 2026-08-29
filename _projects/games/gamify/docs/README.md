---
layout: post
title: Adventure Game - Overview
description: README starting documentation for the adventure game 
category: Gamify
breadcrumb: true
permalink: /gamify/docs/readme
---

## Directory Structure

Project-friendly project organization for the introductory gamify experience.

```text
_projects/gamify/
├── notebook.src.ipynb
├── levels/
│   ├── GameLevelWater.js
│   ├── GameLevelDesert.js
│   ├── GameLevelEnd.js
│   └── GameLevelOverworld.js
├── model/
├── images/
└── docs/
    └── README.md
```

Runtime/distributed outputs are generated into GitHub Pages folders by Makefile:

- _notebooks/projects/gamify/
- _posts/projects/gamify/
- assets/js/projects/gamify/
- images/projects/gamify/

## Development Workflow

Primary SDLC workflow:

Build everything:

```bash
make 
```

Clean up old and build everything:

```bash
make refresh # use when you rename elements
```

Only build priority projects:

```bash
make dev
```

Alternates:

```bash
make -C _projects/gamify build
make -C _projects/gamify docs # docs are not in make dev
```

Validate all registered projects when you need a repo-wide distribution refresh or consistency check.

Use this when:

- Multiple projects were renamed or restructured.
- You want to verify all registered project outputs in one run.
- You want a quick pre-commit sanity check for project distribution.

```bash
make build-registered-projects
make build-registered-docs # docs are not in make dev
```

## CI/CD Targets and Action Logs

GitHub Actions uses the same registered targets:

```yaml
- name: Build registered projects
  run: |
    make build-registered-projects
    make build-registered-docs
```

Expected Actions log lines for project-level visibility:

- 📦 Building project: gamify
- 📚 Building docs for: gamify

If docs verification is enabled in workflow, expect summary lines similar to:

- Registered project docs found: <count>
- Sample generated docs:

These logs are the quickest way to confirm _projects registration and distribution are running in CI.

## Edit/Save Workflow

1. Edit files in _projects/gamify/
2. Save file and let auto-distribution run.
3. Jekyll regenerates affected pages.
4. Refresh browser and validate changes.

## Path Guidance

Use runtime absolute paths in code.

```javascript
// Image path from gameEnv
const sprite = gameEnv.path + '/images/projects/gamify/knight.png';

// Shared game engine import, the @ is changed by jekyll to relative path
import GameControl from '@assets/js/GameEnginev1.1/essentials/GameControl.js';
```

## Registration Model

Project integration into Makefile is registration-based.

1. Add project name to _projects/.makeprojects.
2. Use the project Makefile template targets: build, clean, watch, docs, docs-clean.
3. For new projects, typically only DATE_OF_CREATION and project files change.

No Makefile fragments or project-specific root targets are required.

## Version Control Strategy

Track source files in _projects. Treat files built by make as generated artifacts, they should to be be in GitHub

```gitignore
# Track source
!_projects/gamify/**

# Ignore generated distribution
_notebooks/projects/gamify/
assets/js/projects/gamify/
images/projects/gamify/
_posts/projects/gamify/
```

## Notes

This README is the baseline introduction to the build system concepts for this project. Real-world, deeper references belong in the main README.

For an example of lightweight team documentation, see the sample GameLevelWater write-up:

- [Sample Level Documentation](/gamify/gamelevelwater)
