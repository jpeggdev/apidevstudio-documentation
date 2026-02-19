---
title: Request Inspector
description: Monitor, search, and export all HTTP requests hitting your mock server
---

The Request Inspector captures every HTTP request made to your mock server in real-time, including requests to non-existent endpoints (404s). Use it to debug integrations, verify webhook payloads, and understand how your APIs are being called.

## Viewing Requests

1. Click **Requests** in the sidebar (or press `Ctrl+3`)
2. Requests appear in reverse chronological order (newest first)
3. The list auto-refreshes every 2 seconds

Each request shows:
- HTTP method and path
- Response status code
- Timestamp
- Duration
- Star indicator

## Request Details

Click any request to view its full details:

- **Request headers** - All incoming HTTP headers
- **Request body** - The request payload (JSON-formatted if applicable)
- **Query parameters** - Parsed query string values
- **Response headers** - Headers returned by your mock
- **Response body** - The response that was sent back
- **Metadata** - Timestamp, duration, IP address, endpoint match (or "No match" for 404 responses)

## Searching Requests

Use the search box (`Ctrl+F`) to filter requests by:

- **Path** - Match against the request URL path
- **Body content** - Search within request or response bodies
- **Response content** - Find specific response data

Search is case-insensitive and matches partial strings.

## Filtering

Filter the request list by:

### HTTP Method

Click the method filter dropdown to show only specific methods (GET, POST, PUT, DELETE, etc.).

### Starred Only

Toggle the star filter to show only bookmarked requests.

## Starring Requests

Star important requests to bookmark them for later reference:

- Click the star icon on any request
- Press `S` with a request selected
- Starred requests appear with a yellow star indicator
- Use the "Starred only" filter to find them quickly

## Exporting Requests

Export requests in multiple formats for documentation, debugging, or sharing:

1. Select one or more requests (or use **Select All**)
2. Click **Export**
3. Choose a format:

| Format | Use Case |
|--------|----------|
| **JSON** | Machine-readable, import into other tools |
| **CSV** | Open in spreadsheets for analysis |
| **cURL** | Replay requests from the command line |
| **HAR** | HTTP Archive format for browser dev tools |

## Deleting Requests

- **Single request**: Select and press `Delete`, or click the delete icon
- **All requests**: Press `Ctrl+Shift+Delete` or click **Clear All**

Deleted requests cannot be recovered.

## Tips

- **Auto-refresh**: The request list updates every 2 seconds automatically
- **Keyboard navigation**: Use arrow keys to navigate the list, `Enter` to view details
- **Star webhook payloads**: Star important webhook requests so they do not get lost in the noise
- **Export for documentation**: Export as JSON to include API examples in your docs
- **Use with proxy recording**: When using proxy endpoints, requests show both the original request and the proxied response
