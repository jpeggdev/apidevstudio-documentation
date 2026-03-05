---
title: CLI Reference
description: Command-line interface for API Dev Studio
---


API Dev Studio includes a command-line interface (`apidev`) for managing mock servers, running the MCP server, and performing common tasks without the GUI.

## Installation

The CLI is included with API Dev Studio. After installation, add it to your PATH:

**Windows:**
```
%LOCALAPPDATA%\api-dev-studio\
```

**macOS:**
```
/Applications/API Dev Studio.app/Contents/MacOS/
```

**Linux:**
```
/usr/local/bin/
```

Or download the standalone CLI from the releases page.

## Commands

### `apidev serve`

Start the mock server for a project.

```bash
apidev serve [PROJECT_ID] [OPTIONS]
```

**Options:**
| Option | Description |
|--------|-------------|
| `-p, --port <PORT>` | Port to run server on (default: from project settings) |
| `--host <HOST>` | Host to bind to (default: 127.0.0.1) |

**Examples:**
```bash
apidev serve

apidev serve my-project --port 4000

apidev serve --host 0.0.0.0
```

### `apidev mcp`

Start the MCP server for AI assistant integration.

```bash
apidev mcp [OPTIONS]
```

**Options:**
| Option | Description |
|--------|-------------|
| `--http` | Run in HTTP mode (default: stdio) |
| `-p, --port <PORT>` | HTTP port (default: 3100) |

**Examples:**
```bash
apidev mcp

apidev mcp --http --port 3100
```

### `apidev list`

List projects or endpoints.

```bash
apidev list [RESOURCE]
```

**Resources:**
- `projects` (default) - List all projects
- `endpoints [PROJECT_ID]` - List endpoints in a project

**Examples:**
```bash
apidev list

apidev list endpoints my-project
```

### `apidev import`

Import an OpenAPI specification.

```bash
apidev import <FILE> [OPTIONS]
```

**Options:**
| Option | Description |
|--------|-------------|
| `-p, --project <ID>` | Target project ID |
| `--overwrite` | Overwrite existing endpoints |

**Examples:**
```bash
apidev import api-spec.yaml

apidev import api-spec.json --project my-api --overwrite
```

### `apidev export`

Export a project as OpenAPI specification.

```bash
apidev export <PROJECT_ID> [OPTIONS]
```

**Options:**
| Option | Description |
|--------|-------------|
| `-o, --output <FILE>` | Output file path |
| `-f, --format <FORMAT>` | Format: json or yaml (default: yaml) |

**Examples:**
```bash
apidev export my-project -o api-spec.yaml

apidev export my-project -o api-spec.json --format json
```

### `apidev status`

Show whether the mock server is currently running.

```bash
apidev status
```

### `apidev stop`

Stop the running mock server.

```bash
apidev stop
```

### `apidev requests`

View and manage logged HTTP requests.

```bash
apidev requests <SUBCOMMAND>
```

| Subcommand | Description |
|------------|-------------|
| `list <PROJECT>` | List recent requests (`-l, --limit`, `-m, --method`, `-s, --status`, `--starred`, `--json`) |
| `show <ID>` | Show full request details (`--json`) |
| `delete <ID...>` | Delete specific requests by ID |
| `clear <PROJECT>` | Clear all requests for a project (`-f, --force`) |
| `star <ID>` | Star a request (`--unstar` to remove star) |

**Examples:**
```bash
apidev requests list my-project --limit 20

apidev requests list my-project --method POST --status 5xx

apidev requests show abc123

apidev requests star abc123
```

### `apidev version`

Show version information.

```bash
apidev version
```

### `apidev init`

Initialize a new project in a directory.

```bash
apidev init [PATH] [OPTIONS]
```

**Options:**
| Option | Description |
|--------|-------------|
| `-n, --name <NAME>` | Project name |
| `-p, --port <PORT>` | Port number (default: 3001, range: 1024-65535) |
| `--with-examples` | Add example endpoints (GET /api/users, GET /api/users/:id, POST /api/users, GET /health) |
| `--force` | Overwrite existing files |

**Examples:**
```bash
apidev init

apidev init ./my-api --name "My API" --port 4000 --with-examples
```

Creates `project.json` and `endpoints.json` in the target directory.

### `apidev curl`

Import an endpoint from a cURL command.

```bash
apidev curl <CURL_STRING> [OPTIONS]
```

**Options:**
| Option | Description |
|--------|-------------|
| `-p, --project <PROJECT>` | Target project (required) |
| `-n, --name <NAME>` | Endpoint name (default: auto-generated) |
| `--preview` | Preview only, don't import |

**Examples:**
```bash
apidev curl "curl -X POST https://api.example.com/users -H 'Content-Type: application/json' -d '{\"name\":\"test\"}'" -p my-project

apidev curl "curl https://api.example.com/health" -p my-project --preview
```

### `apidev project`

Manage projects.

```bash
apidev project <SUBCOMMAND>
```

| Subcommand | Description |
|------------|-------------|
| `list` | List all projects (`--json` for JSON output) |
| `create <NAME>` | Create a project (`-p, --port`, `-d, --description`) |
| `show <NAME>` | Show project details (`--json`) |
| `update <NAME>` | Update settings (`--new-name`, `-p, --port`, `-d, --description`) |
| `delete <NAME>` | Delete a project (`-f, --force` to skip confirmation) |

### `apidev endpoint`

Manage endpoints within a project.

```bash
apidev endpoint <SUBCOMMAND>
```

| Subcommand | Description |
|------------|-------------|
| `list <PROJECT>` | List endpoints (`--json`, `--enabled-only`) |
| `add <PROJECT>` | Add endpoint (`-n, --name`, `-p, --path`, `-m, --method`, `-s, --status`, `-b, --body`, `--delay`, `--content-type`) |
| `show <PROJECT> <ENDPOINT>` | Show details (`--json`) |
| `remove <PROJECT> <ENDPOINT>` | Remove endpoint (`-f, --force`) |
| `enable <PROJECT> <ENDPOINT>` | Enable an endpoint |
| `disable <PROJECT> <ENDPOINT>` | Disable an endpoint |

**Example:**
```bash
apidev endpoint add my-project -n "Get Users" -p /api/users -m GET -s 200 -b '{"users":[]}'
```

### `apidev environment`

Manage environments and variables. Requires Pro license.

```bash
apidev environment <SUBCOMMAND>
```

| Subcommand | Description |
|------------|-------------|
| `list <PROJECT>` | List environments (`--json`) |
| `create` | Create environment (`-n, --name`, `-p, --project` optional for global, `--var KEY=VALUE,...`, `--secret KEY,...`) |
| `show <ID>` | Show details (`--json`, `--reveal` to unmask secrets) |
| `update <ID>` | Update (`-n, --name`, `--var`, `--secret`) |
| `delete <ID>` | Delete (`-f, --force`) |
| `activate <PROJECT> [ENV]` | Set active environment (omit ENV to deactivate) |
| `duplicate <ID>` | Clone environment (`-n, --name`) |

See [Environments](../features/environments.md) for details.

### `apidev recording`

Manage proxy recordings.

```bash
apidev recording <SUBCOMMAND>
```

| Subcommand | Description |
|------------|-------------|
| `list <ENDPOINT>` | List recordings for an endpoint (`--json`) |
| `delete <ID>` | Delete a specific recording |
| `clear <ENDPOINT>` | Clear all recordings (`-f, --force`) |
| `count <PROJECT>` | Show recording count for a project |

### `apidev license`

Manage your license.

```bash
apidev license <SUBCOMMAND>
```

| Subcommand | Description |
|------------|-------------|
| `status` | Show current license status |
| `activate <KEY>` | Activate with a license key |
| `activate-email <EMAIL>` | Request email-based activation |
| `check <EMAIL>` | Check activation status after email activation |

### `apidev settings`

View and update application settings.

```bash
apidev settings <SUBCOMMAND>
```

| Subcommand | Description |
|------------|-------------|
| `show` | Show current settings (`--json`) |
| `update` | Update a setting (`--theme`, `--default-port`, `--mcp-port`, `--mcp-auto-start`, `--mcp-logging-mode`, `--confirm-before-delete`, `--developer-mode`, `--error-reporting`) |

### `apidev tunnel`

Manage public URL tunnels. Requires Pro license.

```bash
apidev tunnel <SUBCOMMAND>
```

| Subcommand | Description |
|------------|-------------|
| `start <PROJECT>` | Start a tunnel (`-p, --provider cloudflared\|ngrok`, `-P, --port`) |
| `stop <PROJECT>` | Stop a running tunnel |
| `status <PROJECT>` | Show tunnel status |
| `install` | Check if tunnel binaries are installed |

### `apidev tls`

Manage HTTPS/TLS certificates.

```bash
apidev tls <SUBCOMMAND>
```

| Subcommand | Description |
|------------|-------------|
| `status` | Show certificate status |
| `generate` | Generate a self-signed certificate (Pro) |
| `trust` | Show OS-specific trust instructions |

### `apidev contract`

Contract testing against OpenAPI specs. Requires Pro license.

```bash
apidev contract <SUBCOMMAND>
```

| Subcommand | Description |
|------------|-------------|
| `validate <PROJECT>` | Validate logged requests against a spec (`-s, --spec <FILE>`, `-l, --limit`, `--json`) |
| `status <PROJECT>` | Show validation status (`-s, --spec <FILE>`) |
| `import <PROJECT> <URL>` | Fetch an OpenAPI spec from a URL (`-o, --output <FILE>`) |

## Environment Variables

| Variable | Description |
|----------|-------------|
| `APIDEV_DATA_DIR` | Override default data directory |
| `APIDEV_LOG_LEVEL` | Log level: error, warn, info, debug, trace |

## Exit Codes

| Code | Description |
|------|-------------|
| 0 | Success |
| 1 | General error |
| 2 | Invalid arguments |
| 3 | Project not found |
| 4 | Port already in use |

## Examples

### Start Development Server

```bash
apidev serve my-api --port 3001

curl http://localhost:3001/api/users
```

### CI/CD Integration

```bash
apidev import ./openapi.yaml --project test-api --overwrite
apidev serve test-api --port 3001 &
npm test
```

### Claude Desktop Integration

Add to your Claude Desktop config (`claude_desktop_config.json`):

```json
{
  "mcpServers": {
    "apidevstudio": {
      "command": "apidev",
      "args": ["mcp"]
    }
  }
}
```
