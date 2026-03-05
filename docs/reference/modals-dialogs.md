---
title: Modals & Dialogs
description: Reference for all modals and dialogs in the app
context:
  - modals
  - dialogs
---

# Modals & Dialogs

A complete reference of all modals and dialogs in API Dev Studio.

---

## Project Management

### Create Project Modal

**Trigger**: Click "New Project" button or press `Ctrl+N` in Projects view

Create a new project with:
- **Name**: Project identifier (required)
- **Description**: Optional description
- **Port**: HTTP server port (default: 3001)

### Duplicate Project Modal

**Trigger**: Press `Ctrl+D` on selected project

Duplicate an existing project with all endpoints and configuration. You'll be prompted to:
- Enter a new project name
- Choose a new port

The duplicate includes:
- All endpoints and their configurations
- Response variations
- Project settings (CORS, HTTPS)

### Project Settings Modal

**Trigger**: Click ⚙️ icon on project card

Configure project-specific settings:

**HTTPS/TLS**
- Toggle HTTPS on/off
- View certificate status (fingerprint, expiry)
- Access trust instructions
- Delete certificate

**CORS**
- Enable/disable CORS
- Configure allowed origins
- Configure allowed methods

**Logging**
- Enable/disable request logging
- Set log retention period

### Export Project Modal

**Trigger**: Press `Ctrl+E` on selected project or click Export button

Export your project as a `.apidev.zip` archive containing:
- All endpoints and variations
- Project settings
- Configuration files

**Options**:
- Choose export location
- Include/exclude recordings (optional)

### Import Project Modal

**Trigger**: Click "Import Project" button

Import a project from a `.apidev.zip` archive. Shows:
- Project name and description
- Number of endpoints
- Preview of included data

**Options**:
- Overwrite existing project (if name matches)
- Auto-assign new port if conflict exists

---

## Endpoint Management

### Endpoint Editor Modal

**Trigger**: Click **Create Mock**, **Create Proxy**, or **Create Webhook**; or double-click an existing endpoint

Full endpoint editor with tabs:

**Basic**
- Endpoint type (Mock, Proxy, Webhook)
- Name and description
- HTTP method
- Path with parameters

**Response**
- Status code
- Headers (key-value pairs)
- Response body (with template support)
- Response delay (ms)

**Variations**
- Add multiple response variations
- Set variation mode (static, sequential, random, conditional)
- Configure conditions for conditional responses

**Shortcuts**:
- `Ctrl+S` - Save
- `Esc` - Cancel
- `Ctrl+Enter` - Save and close

### Recordings Modal

**Trigger**: Click "View Recordings" on a proxy endpoint

View all recorded responses for a proxy endpoint:
- Request method and path
- Response status and size
- Timestamp
- Full request/response details

**Actions**:
- Delete individual recordings
- Delete all recordings
- Convert recording to mock endpoint

### Generate Mock Modal

**Trigger**: Click "Generate Mock" on a recording

Convert a proxy recording into a mock endpoint. Handles duplicates:

**If endpoint exists**:
- **Merge**: Add as new variation
- **Update**: Replace existing response
- **Skip**: Cancel and keep existing

**If endpoint doesn't exist**:
- Creates new mock endpoint with recording data

---

## Import

### Import OpenAPI Modal

**Trigger**: Click "Import" → "OpenAPI Specification"

Import endpoints from OpenAPI 3.x specs (JSON or YAML):

**Preview**:
- Expandable tree of endpoints
- Request/response details
- Number of endpoints to import

**Options**:
- Overwrite existing endpoints (by path+method)
- Auto-generate names from operationId

### Postman Import Modal

**Trigger**: Click "Import" → "Postman Collection"

Import from Postman Collection v2.1 JSON files:

**Item Selection**:
- Tree view with folders and requests
- Checkboxes for selective import
- Folder-level selection (with indeterminate state)

**Variable Mapping**:
- Shows Postman variables found
- Maps to template helpers (e.g., `{{$guid}}` → `{{uuid}}`)
- Warns about unmapped variables

**Options**:
- Overwrite existing endpoints
- Preserve folder structure

### cURL Import Modal

**Trigger**: Click "Import" > "cURL Command"

Import an endpoint from a pasted cURL command:

**Live Preview**:
- HTTP method and path
- Headers as key-value pairs
- Request body (JSON formatted)
- Authentication detection (Basic, Bearer)
- Warnings for unrecognized flags

**Features**:
- Real-time parsing with debounce
- Auto-generated endpoint name from URL path
- Editable endpoint name before import

See [cURL Import](../features/curl-import.md) for full details.

### Flow Editor Modal

**Trigger**: Click **Create Flow** or click an existing flow to edit

Create or edit an automation flow with steps:

**Fields**:
- **Name**: Flow name (required)
- **Description**: Optional description

**Steps**: Each step has:
- **Trigger**: When to execute — "When request hits" (endpoint), "After delay" (ms), or "After step" (another step)
- **Action**: What to do — "Return mock response" (endpoint), "Send callback" (HTTP method + URL), or "Proxy forward" (endpoint)
- **Label**: Optional step label

**Controls**:
- **+ Add Step** to add steps
- **Remove** to delete individual steps

See [Flows](../features/flows.md) for full details.

### Replay Modal

**Trigger**: Click **Replay** on a recording session in the **By Session** view

Replay a recorded proxy session against a target URL:

**Configuration**:
- **Target URL**: Base URL to send requests to (recorded paths are appended)
- **Replay Speed**: Instant, 0.5x, 1x (original timing), or 2x
- **Header Overrides**: Optional key-value pairs to add or replace on all requests

**Results**: Shows total, passed, and failed counts with per-request details (method, path, expected/actual status, duration).

See [Session Replay](../features/session-replay.md) for full details.

### JSON Import Modal

**Trigger**: Click **Import** > **JSON (API Dev Studio)**

4-step wizard to import endpoints from an API Dev Studio JSON export file:

1. **Select**: Choose a `.json` file
2. **Preview**: Table of endpoints with type, method, path, name. Option to overwrite existing endpoints.
3. **Import**: Progress indicator while creating endpoints
4. **Summary**: Counts of imported, skipped, and errored endpoints

See [JSON Import](../features/json-import.md) for full details.

### Registry Import Modal

**Trigger**: Click **Import** on an API in the registry browser

Import OpenAPI specs from the API Dev Studio Registry:

**Options**:
- **New project**: Creates a new project (enter name)
- **Existing project**: Adds to a project you select

Shows endpoint count and project name on completion.

See [API Registry Import](../features/api-registry-import.md) for full details.

---

## Export

### Docker Export Modal

**Trigger**: Click **Export** > **Docker**

Export your project's mock endpoints as a Docker-ready package.

**Configuration**:
- **Port**: Server port (defaults to project port)
- **Enable CORS**: Add CORS middleware (default: on)
- **Enable Logging**: Add HTTP request logging (default: on)

**Output**: Generates 7 files in a selected directory:
- `package.json`, `server.js`, `endpoints.json`
- `Dockerfile`, `docker-compose.yml`, `.dockerignore`
- `README.md` with quick-start instructions

The generated package runs a standalone Express.js mock server with template variable support.

### Export Dropdown

**Trigger**: Click "Export" button in Requests or Endpoints view

**Export Formats**:

**Requests**:
- JSON - Machine-readable format
- CSV - Spreadsheet format
- cURL - Command-line commands
- HAR - HTTP Archive format

**Endpoints (OpenAPI)**:
- JSON - OpenAPI 3.0 JSON
- YAML - OpenAPI 3.0 YAML

---

## Licensing

### License Activation Modal

**Trigger**: Click "Activate License" in Settings or "Upgrade to Pro"

Activate your Pro license using:

**Method 1: License Key**
- Enter license key from purchase email
- Validates and activates instantly

**Method 2: Email Link**
- Enter email used for purchase
- Receive activation link via email
- Click link to activate

**License Status Display**:
- Current status (Active/Free)
- Email associated with license
- Machine ID
- Deactivate button (to move to another device)

### Upgrade Prompt Modal

**Trigger**: Click on Pro-only feature without license

Shows:
- List of Pro features
- Current price ($29)
- Link to purchase page
- Option to activate if already purchased

---

## HTTPS/TLS

### Trust Instructions Modal

**Trigger**: Click "View Trust Instructions" in Project Settings

Platform-specific instructions for trusting self-signed certificates:

**Tabs**:
- Windows
- macOS
- Linux

**Contents**:
- Step-by-step instructions
- Certificate file path (with copy button)
- Screenshots (where helpful)
- Troubleshooting tips

---

## Error Reporting

### Error Report Manager

**Trigger**: Settings → Developer section → "View Error Reports" (Developer mode only)

Manage error reports:

**List View**:
- Report ID
- Type (crash, manual, panic)
- Timestamp
- Description

**Actions**:
- View full report (JSON or Markdown)
- Delete individual report
- Delete all reports

### Manual Bug Report Dialog

**Trigger**: Press `Ctrl+Shift+B` or Help → Report a Bug

Submit a manual bug report:

**Fields**:
- Description (required) - What happened?
- Steps to reproduce (optional)
- Expected vs actual behavior (optional)

**Includes automatically**:
- Application state snapshot
- Recent breadcrumbs (last 100 actions)
- System diagnostics
- Error logs

**Privacy**: API keys, passwords, and tokens are redacted.

---

## Utilities

### Settings Modal

**Trigger**: Press `Ctrl+,` or click Settings button

Configure app-wide settings:

**Appearance**
- Theme (Dark/Light/System)
- Animations enabled
- Sidebar collapsed by default

**Server**
- Default port for new projects
- Auto-start server on project create

**Startup**
- Close to system tray
- Start minimized
- Launch on system startup

**Updates**
- View changelog
- Auto-check for updates
- Auto-download updates
- Auto-install updates

**License**
- View license status
- Activate/deactivate license

**Developer** (Developer mode only)
- View error reports
- Developer mode status

### Keyboard Shortcuts Modal

**Trigger**: Press `Ctrl+?` or `F1`

Displays all keyboard shortcuts organized by:
- Global shortcuts
- Navigation
- Per-view shortcuts (Projects, Endpoints, Requests)
- Modal shortcuts

**Features**:
- Searchable/filterable
- Grouped by category
- Platform-specific display (Ctrl vs Cmd)

### Changelog Modal

**Trigger**: Click **Changelog** button in Settings (Updates section)

Displays release notes fetched from GitHub:

- Version number with release date
- Current version highlighted with a "CURRENT" badge
- Markdown-rendered release notes (headers, lists, links, code)
- Link to view all releases on GitHub

### Confirm Dialog

**Trigger**: Various destructive actions

Generic confirmation dialog for:
- Delete project
- Delete endpoint(s)
- Delete request(s)
- Clear all data
- Overwrite existing data

**Options**:
- Confirm (default)
- Cancel (Esc)
- "Don't ask again" checkbox (context-dependent)

**Shortcuts**:
- `Enter` - Confirm
- `Esc` - Cancel

---

## Common Features

### Keyboard Support

All modals support:
- `Esc` to close
- `Tab` / `Shift+Tab` to navigate fields
- `Enter` to submit (when not in textarea)

### Click Outside to Close

Most modals (except confirmation dialogs) close when clicking the backdrop.

### Form Validation

Forms show validation errors:
- Required field indicators (red asterisk)
- Inline error messages
- Submit button disabled until valid

### Responsive Design

All modals are responsive:
- Full-screen on mobile/small windows
- Centered with max-width on desktop
- Scrollable content when too tall
