---
title: Error Reporting
description: Automatic crash capture, manual bug reports, and AI-powered debugging
---

API Dev Studio includes a built-in error reporting system that captures crashes, lets you submit manual bug reports, and integrates with AI assistants for debugging.

## Automatic Crash Reports

When the app encounters an unexpected error, a crash report is automatically generated and saved locally. Reports capture:

- Error type and message
- Stack trace
- Application state at the time of the crash
- Recent actions (breadcrumbs)
- System diagnostics

No data leaves your machine. Reports are stored locally at:
- **Windows**: `%APPDATA%\api-dev-studio\error_reports\`
- **macOS**: `~/Library/Application Support/api-dev-studio/error_reports/`
- **Linux**: `~/.config/api-dev-studio/error_reports/`

## Manual Bug Reports

Submit a bug report at any time to capture the current application state.

### How to Submit

1. Press `Ctrl+Shift+B` (or Help > Report a Bug)
2. Describe what happened
3. Optionally add steps to reproduce
4. Click **Submit**

The report captures your current state and the last 100 breadcrumbs (recent actions), giving context for what led up to the issue.

## Developer Mode

Developer mode enables enhanced debugging capabilities for troubleshooting complex issues.

### Activation

Press `Ctrl+Shift+D` three times on the **Settings** page.

### What Changes in Developer Mode

- Detailed crash reports with full application state
- The MCP `replay_error_report` tool becomes available
- Performance metrics are included in reports
- A **View Error Reports** button appears in Settings
- Email and project name redaction is relaxed (for local debugging)

Developer mode is local-only. No data is transmitted externally.

## Error Report Manager

View and manage all saved error reports.

**Location**: Settings > Developer section > **View Error Reports** (requires Developer mode)

The manager shows:
- Report ID and type (crash, manual, panic)
- Timestamp and description
- Full report in JSON or Markdown format

You can delete individual reports or clear all reports from this view.

## Privacy Redaction

Error reports are sanitized before storage to protect sensitive data.

**Always redacted:**
- API keys (Stripe keys, hex keys, Base64 secrets)
- Passwords and authentication tokens
- Authorization headers and Bearer tokens
- Sensitive query parameters (api_key, token, password, secret)

**Redacted in production mode only:**
- Email addresses
- Project names

**Never redacted:**
- Stack traces and error messages (after token removal)
- File paths, command names, and diagnostic data

## AI-Powered Debugging (MCP)

With Developer mode enabled, you can use the MCP `replay_error_report` tool to have an AI assistant analyze your error reports.

### Workflow

1. Enable Developer mode (`Ctrl+Shift+D` x3 on Settings)
2. Trigger the error or submit a bug report
3. Open Error Reports view and copy the report ID
4. In Claude (or another MCP-connected AI): ask it to use `replay_error_report` with the report ID
5. The AI analyzes the state snapshot and suggests fixes

### What the AI Receives

- Error summary (type, message, timestamp, source location)
- Stack trace
- Recent actions (breadcrumbs with timing)
- Application state at error time
- Detected issues (port conflicts, lock contention, slow operations)
- System diagnostics
- Reproduction steps (inferred from breadcrumbs)

## Breadcrumb Tracking

The error reporting system tracks the last 100 actions leading up to an error:

| Action Type | What Is Tracked |
|-------------|-----------------|
| Tauri commands | Command name, duration, success/failure, error messages |
| Database operations | Table, operation type, rows affected, duration |
| Server events | Project ID, event type, details |
| Endpoint changes | Endpoint ID, action (created/updated/deleted) |
| Navigation | Screen changes |

Breadcrumbs provide the "what happened before the crash" context that makes debugging possible.
