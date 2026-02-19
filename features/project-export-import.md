---
title: Project Export & Import
description: Share projects as portable .apidev.zip archives
---

Export your projects as portable archive files and import them on another machine or share them with teammates.

## Exporting a Project

1. Select the project you want to export
2. Press `Ctrl+E` or click the **Export** button
3. Choose a save location
4. The project is saved as a `.apidev.zip` file

### What Is Included

The export archive contains:
- All endpoints and their configurations
- Response variations
- Project settings (port, CORS, HTTPS config)
- Folder structure

### What Is Not Included

- Request history (stored in local.db, may contain sensitive data)
- Recordings (optional, can be included)
- TLS certificates (regenerated on import)

## Importing a Project

1. Click **Import Project** in the project toolbar
2. Select a `.apidev.zip` file
3. Preview the project details:
   - Project name and description
   - Number of endpoints
   - Included configuration
4. Choose import options:
   - **Overwrite existing**: Replace a project with the same name
   - **Auto-assign port**: Pick a new port if the original port is in use
5. Click **Import**

The imported project appears in your sidebar and is ready to use.

## Use Cases

### Team Collaboration

Share a set of mock endpoints with your team:

1. Export your project
2. Share the `.apidev.zip` file (email, Slack, Git repo)
3. Teammates import the file to get an identical mock setup

### Backup

Regularly export important projects as backups:

1. Export each project
2. Store the `.apidev.zip` files in a safe location
3. Import to restore if anything goes wrong

### Environment Portability

Move your mock setup between machines:

1. Export on your work machine
2. Import on your home machine or CI server
3. All endpoints and settings are preserved

## CLI Export/Import

You can also export and import via the CLI:

```bash
# Export
apidev export my-project -o my-project.apidev.zip

# Import
apidev import my-project.apidev.zip --project my-api
```

See the [CLI Reference](../reference/cli) for full details.
