---
title: Flows
description: Automate multi-step API workflows with triggers and actions
context:
  - flow-editor
  - endpoint-editor
---

# Flows

Flows let you define multi-step API workflows that chain triggers and actions together. Use flows to simulate complex scenarios like payment callbacks, webhook chains, or delayed responses.

## Creating a Flow

1. Open a project
2. Click **Create Flow**
3. Enter a **Name** (e.g., "Stripe Payment Flow")
4. Optionally add a **Description**
5. Add one or more steps
6. Click **Create Flow**

## Steps

Each flow consists of one or more steps. A step pairs a **trigger** (when to run) with an **action** (what to do).

### Trigger Types

| Trigger | Description | Configuration |
|---------|-------------|---------------|
| **When request hits** | Fires when a specific endpoint receives a request | Select an endpoint |
| **After delay** | Fires after a configurable delay | Delay in milliseconds |
| **After step** | Fires after another step in the flow completes | Select a step |

### Action Types

| Action | Description | Configuration |
|--------|-------------|---------------|
| **Return mock response** | Sends the configured mock response for an endpoint | Select a mock endpoint |
| **Send callback (HTTP)** | Makes an outbound HTTP request to an external URL | HTTP method and URL |
| **Proxy forward** | Forwards the request through a proxy endpoint | Select a proxy endpoint |

## Adding Steps

1. In the flow editor, click **+ Add Step**
2. Select a trigger type and configure it
3. Select an action type and configure it
4. Optionally add a label to identify the step

Steps are displayed in order with a visual timeline connector.

## Enable and Disable

Flows can be toggled on or off. A disabled flow does not execute when its triggers fire. Toggle the flow's **Enabled** state from the flow list.

## Editing a Flow

1. Click on an existing flow to open the editor
2. Modify the name, description, or steps
3. Click **Save Changes**

## Deleting a Flow

1. Select a flow from the list
2. Click **Delete**
3. Confirm the deletion

## Example: Webhook Callback

Simulate an API that accepts a payment and sends a webhook callback after processing:

1. **Step 1**: Trigger = "When request hits" on `POST /payments`, Action = "Return mock response" (202 Accepted)
2. **Step 2**: Trigger = "After delay" (2000ms), Action = "Send callback" (POST to `https://yourapp.com/webhooks/payment`)

This returns an immediate 202 response, then sends a callback 2 seconds later — matching how real payment APIs behave.
