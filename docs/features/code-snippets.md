---
title: Code Snippets
description: Copy endpoint calls as cURL, fetch, axios, or Python code
---

Generate ready-to-use code snippets for any endpoint in your project. Right-click an endpoint or use the **Copy as Code** button to get a working request in your language of choice.

## Supported Formats

| Format | Language | Use Case |
|--------|----------|----------|
| **cURL** | Shell | Command-line testing, documentation |
| **fetch** | JavaScript | Browser and Node.js applications |
| **axios** | JavaScript | Popular HTTP client for Node.js/browser |
| **Python** | Python | Python `requests` library |

## How to Use

### From the Endpoint Tree

1. Right-click an endpoint in the tree view
2. Select **Copy as Code**
3. Choose your format
4. The snippet is copied to your clipboard

### From the Endpoint Editor

1. Open an endpoint for editing
2. Click the **Copy as Code** dropdown in the toolbar
3. Select a format
4. The snippet is copied to your clipboard

## Generated Snippets

Each snippet includes:

- The correct HTTP method
- The full URL with your server's base URL and the endpoint path
- `Content-Type: application/json` header for POST/PUT/PATCH requests
- A request body template (simplified from your mock response, with template variables stripped)

### Example: cURL

```bash
curl -X GET http://localhost:3001/api/users
```

### Example: fetch

```javascript
fetch('http://localhost:3001/api/users')
  .then(response => response.json())
  .then(data => console.log(data));
```

### Example: axios

```javascript
axios.get('http://localhost:3001/api/users')
  .then(response => console.log(response.data));
```

### Example: Python

```python
import requests

response = requests.get('http://localhost:3001/api/users')
print(response.json())
```

## Tips

- **Quick sharing**: Copy a cURL snippet to share an endpoint call with a teammate
- **Documentation**: Paste generated snippets into your API docs as usage examples
- **Request bodies**: For POST/PUT/PATCH endpoints, the snippet includes a body template based on your mock response schema
