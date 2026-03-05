---
title: cURL Import
description: Create mock endpoints by pasting cURL commands from your browser or docs
---

Import API requests by pasting cURL commands directly. This is the fastest way to create a mock endpoint from a real API call -- copy a cURL command from your browser DevTools, API documentation, or terminal, and API Dev Studio creates a mock endpoint from it.

## How to Import

1. Click **Import** in the project toolbar
2. Select **cURL Command**
3. Paste your cURL command into the text area
4. The command is parsed in real-time with a live preview
5. Optionally edit the generated endpoint name
6. Click **Import**

A new mock endpoint is created with the method, path, and headers extracted from the cURL command.

## What Gets Parsed

The cURL parser extracts:

| Component | Source |
|-----------|--------|
| **HTTP method** | `-X` / `--request` flag, or inferred from other flags |
| **URL path** | URL argument |
| **Headers** | `-H` / `--header` flags |
| **Request body** | `-d` / `--data` / `--data-raw` flags |
| **Query parameters** | Extracted from the URL query string |
| **Authentication** | `-u` / `--user` (Basic auth) or `Authorization` header (Bearer) |

## Supported Formats

The parser handles cURL commands from various sources:

### Browser DevTools

Right-click a request in Chrome/Firefox DevTools Network tab and select "Copy as cURL":

```bash
curl 'https://api.example.com/users' \
  -H 'Accept: application/json' \
  -H 'Authorization: Bearer eyJhbG...'
```

### Multi-line Commands

Backslash-continued commands are handled:

```bash
curl -X POST https://api.example.com/users \
  -H 'Content-Type: application/json' \
  -d '{"name": "Alice", "email": "alice@example.com"}'
```

### Windows-style Commands

Commands using `^` for line continuation are supported:

```bash
curl -X POST https://api.example.com/users ^
  -H "Content-Type: application/json" ^
  -d "{\"name\": \"Alice\"}"
```

## Live Preview

As you type or paste, the modal shows a live preview of the parsed result:

- **Method** and **path** extracted from the command
- **Headers** listed as key-value pairs
- **Body** formatted if JSON is detected
- **Warnings** for any unrecognized flags or issues

If the command cannot be parsed, an error message explains what went wrong with a suggestion for how to fix it.

## Tips

- **Copy from browser**: Right-click any network request in DevTools and select "Copy as cURL" for the quickest workflow
- **Auto-naming**: The endpoint name is auto-generated from the URL path. You can change it before importing.
- **Body handling**: For POST/PUT/PATCH requests, the request body from the cURL command is preserved for reference
- **Auth detection**: Basic auth (`-u user:pass`) and Bearer tokens are detected and shown in the preview
