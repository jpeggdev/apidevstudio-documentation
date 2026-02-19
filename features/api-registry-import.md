---
title: API Registry Import
description: Import endpoints from the API Dev Studio Registry
context:
  - import-modal
  - endpoint-editor
---

# API Registry Import

Import API specifications from the API Dev Studio Registry directly into your project. The registry provides pre-built OpenAPI specs that you can import as mock endpoints with one click.

API Registry Import is a Pro feature.

## Import Modes

When importing from the registry, choose where to place the endpoints:

| Mode | Description |
|------|-------------|
| **New project** | Creates a new project with a name you specify (defaults to the API name) |
| **Existing project** | Adds the endpoints to a project you select from the dropdown |

## Import Process

1. Browse or search the API registry
2. Click **Import** on an API
3. Choose import mode: **New project** or **Existing project**
4. If new, enter a project name. If existing, select the target project.
5. Click **Import**
6. The spec is fetched, parsed, and converted into mock endpoints

## Results

After import completes, you see:

- The number of endpoints imported
- The project name
- Options to **Close** or **Go to Project** to start working with the imported endpoints
