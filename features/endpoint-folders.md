---
title: Endpoint Folders
description: Organize endpoints into a tree view with collapsible folders
---

As your project grows, the flat endpoint list can become difficult to navigate. API Dev Studio automatically organizes your endpoints into a tree view based on their URL paths, giving you a folder-like hierarchy.

## How It Works

Endpoints are grouped into folders based on shared path segments. For example:

```
/api/users          --> api/ > users/
/api/users/{id}     --> api/ > users/
/api/posts          --> api/ > posts/
/api/posts/{id}     --> api/ > posts/
```

This creates a tree:

```
api/
  users/
    GET /api/users
    GET /api/users/{id}
  posts/
    GET /api/posts
    GET /api/posts/{id}
```

## Using the Tree View

### Expanding and Collapsing

- Click the chevron next to a folder to expand or collapse it
- Press the right arrow key to expand the selected folder
- Press the left arrow key to collapse the selected folder
- Press Space to toggle the folder

### Expand/Collapse All

Use the toolbar buttons or the right-click context menu to expand all or collapse all folders at once.

### Persistent State

Folder expand/collapse state is remembered between sessions. When you reopen the app, your folders are in the same state you left them.

## Context Menu

Right-click a folder or endpoint for additional options:

### On Folders
- **Add Endpoint** -- Create a new endpoint pre-filled with the folder's path prefix
- **Delete Path** -- Delete all endpoints under this folder

### On Endpoints
- **Edit** -- Open the endpoint editor
- **Toggle Enabled** -- Enable or disable the endpoint
- **Copy as Code** -- Generate a code snippet (cURL, fetch, axios, Python)
- **View Recordings** -- Open recordings for proxy endpoints
- **Delete** -- Delete the endpoint

## Multi-Selection

Select multiple endpoints for bulk operations:

- **Click** to select a single endpoint
- **Ctrl+Click** to add to selection
- **Ctrl+A** to select all endpoints
- **Ctrl+Shift+A** to deselect all
- **Delete** to delete all selected endpoints

## Search

Use the search box to filter endpoints. The tree view collapses to show only matching endpoints and their parent folders, making it easy to find specific endpoints in large projects.

## Tips

- **Consistent paths**: Use consistent path prefixes (e.g., `/api/v1/...`) to get clean folder groupings
- **Path parameters**: Endpoints with path parameters like `{id}` are grouped with their collection endpoints
- **Quick add**: Right-click a folder and select "Add Endpoint" to create an endpoint with the path prefix pre-filled
