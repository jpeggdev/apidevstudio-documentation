---
title: JSON Import
description: Import endpoints from API Dev Studio JSON export files
context:
  - import-modal
  - endpoint-editor
---

# JSON Import

Import endpoints from an API Dev Studio JSON export file (`.json`). This completes the round-trip with the JSON export feature, letting you move endpoints between projects or share them with teammates.

## How to Import

The import follows a 4-step wizard:

### Step 1: Select File

1. Click **Import** in the toolbar
2. Select **JSON (API Dev Studio)**
3. Click **Select JSON File** or click the drop zone
4. Choose a `.json` file exported from API Dev Studio

### Step 2: Preview

The preview shows a table of endpoints that will be imported:

| Column | Description |
|--------|-------------|
| **Type** | Endpoint type (mock, proxy, webhook) |
| **Method** | HTTP method (GET, POST, etc.) |
| **Path** | URL path |
| **Name** | Endpoint name |

**Overwrite existing endpoints** — Check this option to replace endpoints that already exist with the same path and method. When unchecked, duplicates are skipped.

### Step 3: Import

Click **Import N Endpoints** to start. A progress indicator shows while endpoints are being created.

### Step 4: Results

The summary shows three counts:

| Count | Description |
|-------|-------------|
| **Imported** | Endpoints successfully created |
| **Skipped** | Endpoints that already existed (when overwrite is off) |
| **Errors** | Endpoints that failed to import |

Lists of imported and skipped endpoint paths are shown for review.

## File Format

The JSON export file uses the `apidevstudio-endpoints` format:

```json
{
  "format": "apidevstudio-endpoints",
  "version": "1.0",
  "exported_at": "2026-01-15T10:30:00Z",
  "project_name": "My API",
  "endpoints": [
    {
      "type": "mock",
      "name": "Get Users",
      "path": "/api/users",
      "method": "GET",
      "enabled": true,
      "config": { ... },
      "operation_id": null,
      "folder_path": ""
    }
  ]
}
```

## Related

- [Project Export & Import](./project-export-import.md) — Export/import entire projects as `.apidev.zip` archives
- [OpenAPI](./openapi.md) — Import from OpenAPI specifications
- [Postman Import](./postman-import.md) — Import from Postman collections
