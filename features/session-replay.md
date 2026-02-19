---
title: Session Replay
description: Replay recorded proxy sessions against real APIs to verify behavior
context:
  - recordings-list
  - proxy-config
---

# Session Replay

Session replay lets you re-send a recorded sequence of proxy requests against a target URL and compare the results. Use it to verify that an API still behaves as expected, or to run recorded traffic against a different environment.

## Prerequisites

Before replaying, you need recorded sessions from [Proxy & Recording](./proxy-recording). When recording is enabled on a proxy endpoint, requests are grouped into sessions automatically.

## Viewing Sessions

1. Open a proxy endpoint
2. Click the **Recordings** tab
3. Switch to the **By Session** view using the toggle in the header
4. Each session card shows the request count and time range

Click a session to expand it and see the individual recordings.

## Starting a Replay

1. In the **By Session** view, click **Replay** on a session
2. Configure the replay settings (see below)
3. Click **Start Replay**

## Configuration

| Setting | Description |
|---------|-------------|
| **Target URL** | The base URL to send requests to (e.g., `https://api.example.com`). Recorded request paths are appended to this URL. |
| **Replay Speed** | Controls the timing between requests. Options: **Instant** (send all at once), **0.5x**, **1x** (original timing), **2x** (double speed). |
| **Header Overrides** | Optional headers to add or replace on every replayed request (e.g., a new `Authorization` token). |

## Results

After replay completes, you see a summary:

- **Total** requests replayed
- **Passed** — actual response status matched the recorded status
- **Failed** — status code mismatch or request error

Each request shows:
- Pass/fail status
- HTTP method and path
- Expected vs actual status code
- Response time in milliseconds
- Error message (if failed)

Click **Run Again** to replay with different settings, or **Close** to dismiss.

## Use Cases

- **Regression testing** — Record a session against your API, then replay after changes to check for regressions
- **Environment comparison** — Replay the same session against staging and production to compare behavior
- **Load simulation** — Use **Instant** speed to send all recorded requests at once
- **Auth rotation** — Replay with updated `Authorization` headers without re-recording
