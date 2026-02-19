---
title: Postman Collection Import
description: Import Postman collections with folder structure and variable mapping
---

Import Postman Collection v2.1 files to quickly create mock endpoints from your existing Postman workspace. API Dev Studio preserves folder structure, maps Postman dynamic variables to template helpers, and lets you select which requests to import.

## How to Import

1. Click **Import** in the project toolbar
2. Select **Postman Collection**
3. Choose your exported collection file (`.json`)
4. Preview the collection contents
5. Select which requests to import
6. Click **Import**

## Collection Preview

The preview shows your Postman collection as a tree:

- **Folders** appear as expandable groups with request counts
- **Requests** show the HTTP method and name
- **Checkboxes** on each item let you include or exclude it

### Selective Import

- Click folder checkboxes to select/deselect entire folders
- Click individual request checkboxes for fine-grained control
- Folder checkboxes show an indeterminate state when some (but not all) children are selected
- Use **Select All** / **Deselect All** for bulk operations

## Variable Mapping

Postman dynamic variables (like `{{$guid}}`) are automatically mapped to API Dev Studio template helpers. Over 26 variables are supported:

| Postman Variable | Template Helper |
|-----------------|----------------|
| `{{$guid}}` | `{{uuid}}` |
| `{{$randomEmail}}` | `{{email}}` |
| `{{$randomFirstName}}` | `{{firstName}}` |
| `{{$randomLastName}}` | `{{lastName}}` |
| `{{$randomFullName}}` | `{{name}}` |
| `{{$randomUserName}}` | `{{username}}` |
| `{{$randomPhoneNumber}}` | `{{phone}}` |
| `{{$randomInt}}` | `{{number 1 1000}}` |
| `{{$randomBoolean}}` | `{{boolean}}` |
| `{{$randomCity}}` | `{{city}}` |
| `{{$randomCountry}}` | `{{country}}` |
| `{{$randomStreetAddress}}` | `{{address}}` |
| `{{$randomCompanyName}}` | `{{company}}` |
| `{{$randomJobTitle}}` | `{{jobTitle}}` |
| `{{$randomUrl}}` | `{{url}}` |
| `{{$randomDomainName}}` | `{{domain}}` |
| `{{$randomIP}}` | `{{ipv4}}` |
| `{{$randomLoremSentence}}` | `{{sentence}}` |
| `{{$randomLoremParagraph}}` | `{{lorem}}` |
| `{{$randomLoremWord}}` | `{{word}}` |
| `{{$timestamp}}` | `{{timestamp}}` |
| `{{$isoTimestamp}}` | `{{datetime}}` |

### Unmapped Variables

If your collection uses Postman environment or collection variables that cannot be auto-mapped, they are shown as warnings in the preview. You can:

- Replace them with template helpers after import
- Leave them as-is (they will appear literally in responses)

## Import Options

| Option | Description |
|--------|-------------|
| **Overwrite existing** | Replace endpoints with matching method + path combinations |
| **Preserve folders** | Maintain Postman folder structure as endpoint folders |

## What Gets Imported

From each Postman request:

- **HTTP method** (GET, POST, PUT, DELETE, etc.)
- **URL path** (extracted from the request URL)
- **Request name** (used as endpoint name)
- **Response body** (from saved example responses, if any)
- **Headers** (converted to response headers)

## Exporting from Postman

To export a collection from Postman:

1. Open Postman
2. Right-click your collection in the sidebar
3. Select **Export**
4. Choose **Collection v2.1** format
5. Save the JSON file
6. Import it into API Dev Studio

## Tips

- **Start with a collection**: If you already have Postman collections for your APIs, import them to instantly create matching mocks
- **Check variable warnings**: Review unmapped variable warnings before importing to avoid literal `{{$variableName}}` strings in your responses
- **Folder structure**: Postman folder hierarchy maps to API Dev Studio's endpoint folder organization
