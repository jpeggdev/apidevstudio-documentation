---
title: Contract Validation
description: Validate API requests against OpenAPI specifications to catch schema drift
---

Contract validation lets you verify that the requests and responses flowing through your mock server conform to an OpenAPI specification. This helps catch schema drift, missing fields, and type mismatches before they reach production.

**This is a Pro feature.** [Upgrade to Pro](./licensing.md) to unlock contract validation.

## How It Works

1. You link an OpenAPI spec to your project
2. API Dev Studio validates each request/response pair against that spec
3. You see a summary of passes, failures, and warnings

Validation checks include:
- **Status codes** -- Does the response status match what the spec declares?
- **Content types** -- Is the Content-Type header correct?
- **Required fields** -- Are all required fields present in the response body?
- **Field types** -- Do field values match their declared types (string, number, boolean, etc.)?
- **String patterns** -- Do string values match any regex patterns defined in the spec?
- **Enum values** -- Are enum fields set to one of the allowed values?
- **Array items** -- Do array elements conform to the declared item schema?
- **Object schemas** -- Does the overall object structure match the spec?

## Setting Up Contract Validation

1. Select your project
2. Navigate to the **Validate** view in the sidebar
3. Click **Set Spec** and select an OpenAPI spec file (JSON or YAML)
4. The spec is linked to your project

Once linked, validation runs against logged requests automatically.

## Viewing Results

The Validate view shows:

- **Summary** -- Total checked, passed, failed, warnings, and skipped counts
- **Results list** -- Each validated request with its status (Pass, Fail, Warn, Skipped)
- **Check details** -- Expand any result to see individual checks with expected vs actual values

### Validation Statuses

| Status | Meaning |
|--------|---------|
| **Pass** | Request/response fully conforms to the spec |
| **Fail** | One or more checks failed (schema mismatch) |
| **Warn** | Non-critical issues detected (e.g., undocumented fields) |
| **Skipped** | Could not validate (e.g., no matching spec path) |

## Validating Individual Requests

You can validate a specific request against the contract:

1. Go to the **Requests** view
2. Select a request
3. Click **Validate** to check it against the linked spec

## Use Cases

### Catching Schema Drift

When your API evolves, mock responses can fall out of sync with the actual spec. Contract validation flags these mismatches:

- A required field was added to the spec but your mock does not return it
- A field type changed from string to number
- An enum gained new values that your mock does not produce

### API-First Development

Define your API contract (OpenAPI spec) first, then validate your mocks against it as you build:

1. Write the OpenAPI spec
2. Create mock endpoints
3. Link the spec and run validation
4. Fix any mismatches
5. Share validated mocks with frontend teams

### CI/CD Integration

Use the CLI to validate contracts in your pipeline:

```bash
apidev serve my-project --port 3001 &
# Run tests against the mock server
# Validation results are logged for review
```

## Troubleshooting

### "No contract spec configured"

You need to link an OpenAPI spec file to your project. Open the Validate view and click **Set Spec**.

### "Failed to read contract spec file"

The linked spec file may have been moved or deleted. Re-link the spec by clicking **Set Spec** again.

### Validation shows "Skipped" for all requests

This usually means the request paths do not match any paths defined in your OpenAPI spec. Check that:
- The spec covers the paths your mock server uses
- Path parameter formats match (e.g., `/users/{id}` in spec vs `/users/{userId}` in endpoint)
