---
title: Environments
description: Manage variables across projects with project-scoped and global environments
context:
  - environment-manager
  - template-variables
---

# Environments

Environments let you define named sets of variables and switch between them. Use environments to manage API keys, base URLs, feature flags, and other values that change between development, staging, and production.

Environments is a Pro feature.

## Creating an Environment

1. Open the **Environments** panel from the sidebar
2. Click **Create Environment**
3. Enter a name (e.g., "Development", "Staging", "Production")
4. Add variables as key-value pairs
5. Click **Save**

## Project vs Global Environments

Environments come in two scopes:

| Scope | Description |
|-------|-------------|
| **Project** | Tied to a specific project. Only visible within that project. |
| **Global** | Available across all projects. Useful for shared credentials or base URLs. |

To create a global environment, omit the project when creating via CLI or select **Global** in the UI.

## Managing Variables

Each environment contains a list of variables with these properties:

| Property | Description |
|----------|-------------|
| **Key** | Variable name (e.g., `API_KEY`, `BASE_URL`) |
| **Value** | Variable value |
| **Secret** | When enabled, the value is masked in the UI |
| **Enabled** | Toggle a variable on/off without deleting it |

To add a variable, click **Add Variable** in the environment editor. To remove one, click the delete button on that row.

## Secret Variables

Mark a variable as **Secret** to mask its value in the UI. Secret values display as `********` and are only revealed with an explicit action (the `--reveal` flag in the CLI). This is useful for API keys, tokens, and passwords.

## Setting the Active Environment

Each project can have one active environment at a time. The active environment provides its variables to template resolution, proxy target URLs, and authentication fields.

1. Select an environment from the list
2. Click **Set Active**

The active environment is indicated with a green dot in the sidebar.

To deactivate, click the active environment and select **Deactivate**.

## Using Environment Variables in Templates

Reference environment variables in response bodies, headers, and URLs with the `{{env.VAR_NAME}}` syntax:

```json
{
  "api_key": "{{env.API_KEY}}",
  "base_url": "{{env.BASE_URL}}"
}
```

If no environment is active or the variable is not defined, `{{env.VAR_NAME}}` resolves to an empty string.

See [Template Variables](./template-variables) for more on template syntax.

## Import and Export

### Import from .env File

1. Open the environment editor
2. Click **Import**
3. Select **From .env file**
4. Choose your `.env` file

Variables are parsed from the standard `KEY=VALUE` format, one per line.

### Import from Postman

1. Open the environment editor
2. Click **Import**
3. Select **From Postman**
4. Choose a Postman environment JSON export

### Export to .env

1. Select an environment
2. Click **Export**
3. Choose a save location

The environment is exported in standard `.env` format.

## Duplicating an Environment

1. Select an environment
2. Click **Duplicate**
3. A copy is created with "(Copy)" appended to the name
4. Edit the copy to adjust values for a different context

## CLI Commands

Manage environments from the command line with `apidev environment`:

```bash
# List environments for a project
apidev environment list my-project

# Create with variables
apidev environment create --name Production --project my-project \
  --var API_KEY=sk-123,BASE_URL=https://api.example.com \
  --secret API_KEY

# Show details (secrets masked by default)
apidev environment show <id>
apidev environment show <id> --reveal

# Set active environment
apidev environment activate my-project <environment-id>

# Deactivate
apidev environment activate my-project

# Duplicate
apidev environment duplicate <id> --name "Production Copy"

# Delete
apidev environment delete <id>
```

See [CLI Reference](../reference/cli) for the full command list.
