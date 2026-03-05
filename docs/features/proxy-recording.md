---
title: Proxy & Recording
description: Proxy requests to real APIs and record responses for mock generation
context:
  - endpoint-editor
  - proxy-config
  - recordings-list
---

# Proxy & Recording

API Dev Studio can proxy requests to real APIs and record the responses. This lets you:

- Capture real API behavior automatically
- Generate mocks from recorded responses
- Switch between live and mock modes

## Creating a Proxy Endpoint

1. Click **Create Proxy**
2. Configure:
   - **Path**: The path to proxy (e.g., `/api/users`)
   - **Target URL**: The real API URL (e.g., `https://api.example.com/users`)
3. Save the endpoint

## How Proxying Works

When a request hits your proxy endpoint:

1. API Dev Studio forwards the request to the target URL
2. The real API responds
3. API Dev Studio returns that response to the caller
4. The request/response is logged (and optionally recorded)

## Recording Mode

Enable recording to capture responses for mock generation:

1. Open your proxy endpoint
2. Toggle **Recording** on
3. Make requests through the proxy
4. Responses are saved to the Recordings tab

## Viewing Recordings

1. Select your proxy endpoint
2. Click the **Recordings** tab
3. See all captured responses with timestamps

Each recording shows:
- Request method and path
- Response status code
- Response body
- Timestamp

## Recording Sessions

Recordings are automatically grouped into sessions based on when they were captured. Switch between two views in the Recordings tab:

- **All** — Flat list of every recording
- **By Session** — Recordings grouped by session, showing request count and time range per session

Click a session to expand it and see individual recordings. Sessions can also be replayed against a target URL — see [Session Replay](./session-replay.md) for details.

## Generate Mocks from Recordings

Convert recordings into mock endpoints:

1. In the Recordings tab, select one or more recordings
2. Click **Generate Mock**
3. Configure the mock endpoint:
   - **Name** — Display name for the endpoint
   - **Path** — URL path for the mock
   - **Method** — HTTP method
   - **Disable proxy after** — Optionally disable the proxy endpoint after generating
4. Choose how to handle duplicates:
   - **Merge**: Combine as response variations
   - **Update**: Replace existing mock
   - **Skip**: Keep existing, ignore new

The generated mock uses the recorded response as its body. Endpoints are reloaded automatically after generation, so the new mock is available immediately without restarting the server.

## Live vs Mock Mode

Toggle between live (proxy) and mock modes:

- **Live Mode**: Requests go to the real API
- **Mock Mode**: Requests return recorded responses as mocks

This lets you develop against real data, then switch to mocks for offline work or testing edge cases.

### Mock Selection Strategies

When in mock mode, configure how recorded responses are selected:

| Strategy | Behavior |
|----------|----------|
| **Most Recent** | Returns the most recently recorded response (default) |
| **Random** | Randomly selects from available recordings |
| **Sequential** | Cycles through recordings in order |
| **Match Field** | Matches a request field to a response field for targeted replay |

Configure the selection strategy in the proxy endpoint's settings under **Mock Selection**.

## Path Rewriting

Rewrite the forwarded URL path using dynamic values. Set a **Path Rewrite** template on your proxy endpoint to replace the default path when forwarding requests.

Supports two types of substitution:

- **Path parameters**: `{param}` -- replaced with extracted path parameter values
- **Environment variables**: `{{env.VAR}}` -- replaced with the active environment variable

**Example:** A proxy endpoint at `/api/items/{id}` with path rewrite `/v2/items/{id}` forwards requests to the target URL using the rewritten path, substituting the captured `id` value.

## Best Practices

1. **Start with proxy**: Begin by proxying the real API
2. **Record key scenarios**: Capture success, error, and edge cases
3. **Generate mocks**: Convert recordings to mocks
4. **Enhance mocks**: Add template variables for dynamic data
5. **Switch to mock mode**: Develop offline with realistic data
