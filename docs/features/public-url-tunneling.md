---
title: Public URL Tunneling
description: Create a public tunnel to expose your local mock server via Cloudflared or Ngrok
---

Create a public tunnel to expose your local mock server to the internet. This is useful for testing webhooks from external services, sharing your mocks with teammates, or testing mobile apps against your local server.

## Supported Providers

API Dev Studio supports two tunnel providers:

| Provider | Setup | Authentication |
|----------|-------|---------------|
| **Cloudflared** | Auto-download available | No account required |
| **Ngrok** | Manual install | Account required |

## Starting a Tunnel

1. Select your project and make sure the server is running
2. Click the **Create Public Tunnel** button
3. Choose your provider (Cloudflared or Ngrok)
4. Confirm to start the tunnel
5. Copy the public URL from the dialog

Your mock server is now accessible at a public URL like `https://random-name.trycloudflare.com`.

## Cloudflared (Recommended)

Cloudflared is the default tunnel provider. It requires no account or authentication.

### Auto-Download

If Cloudflared is not installed on your system, API Dev Studio will offer to download it automatically:

1. Click the **Create Public Tunnel** button
2. If Cloudflared is not detected, click **Download Cloudflared**
3. The binary is downloaded to your app data directory
4. Start the tunnel as normal

### Manual Install

You can also install Cloudflared manually:

**Windows:**
```bash
winget install Cloudflare.cloudflared
```

**macOS:**
```bash
brew install cloudflared
```

**Linux:**
```bash
sudo apt install cloudflared
# or download from https://github.com/cloudflare/cloudflared/releases
```

## Ngrok

Ngrok requires an account and auth token.

### Setup

1. Create an account at [ngrok.com](https://ngrok.com)
2. Install Ngrok and authenticate:
   ```bash
   ngrok config add-authtoken YOUR_TOKEN
   ```
3. Select Ngrok as your tunnel provider in API Dev Studio

## Stopping a Tunnel

1. Click the tunnel button (which shows the active tunnel status when running)
2. Click **Stop Tunnel**

Tunnels are automatically stopped when you stop the project server or close the app.

## Use Cases

### Testing Webhooks

Many external services (Stripe, GitHub, Slack) need to send webhooks to a publicly accessible URL. Use a tunnel to receive webhooks on your local machine:

1. Create a webhook endpoint in your project
2. Start a tunnel
3. Copy the public URL
4. Configure the external service to send webhooks to `https://your-tunnel-url.com/webhooks/stripe`

### Sharing with Teammates

Share your mock API with a teammate for testing:

1. Start a tunnel
2. Send the public URL to your teammate
3. They can make requests against your mocks from their machine

### Mobile Testing

Test your mobile app against local mocks:

1. Start a tunnel
2. Configure your mobile app to use the public URL
3. Test without needing your phone on the same network

## Troubleshooting

### Tunnel Won't Start

**Check:**
1. Your server is running (tunnel requires an active server)
2. You have internet connectivity
3. The tunnel binary is installed and accessible

### Cloudflared Not Detected

If API Dev Studio cannot find Cloudflared:
1. Try the auto-download option
2. Or install it manually and ensure it is in your system PATH
3. Restart API Dev Studio after installation

### Ngrok Authentication Error

Make sure your Ngrok auth token is configured:
```bash
ngrok config add-authtoken YOUR_TOKEN
```

### Public URL Not Accessible

1. Check that the tunnel status shows "Connected"
2. Try the URL in an incognito browser window
3. Some corporate networks may block tunnel traffic
