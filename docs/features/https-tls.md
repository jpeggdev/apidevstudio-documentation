---
title: HTTPS/TLS Support
description: Enable HTTPS for your mock servers with self-signed certificates
context:
  - project-settings
  - https
---

# HTTPS/TLS Support

Enable HTTPS for your mock servers to test secure connections locally. API Dev Studio generates self-signed certificates for each project.

## Enabling HTTPS

1. Select your project
2. Click the **Settings** icon (⚙️)
3. Toggle **Enable HTTPS** on
4. Certificate is generated automatically
5. Click **View Trust Instructions** for setup

Your server will now run on `https://localhost:{port}` instead of `http://localhost:{port}`.

## Trusting the Certificate

Browsers and API clients won't trust self-signed certificates by default. You'll see warnings like "Your connection is not private" or "SSL certificate problem".

To fix this, you need to trust the certificate on your system:

### Windows

1. Click **View Trust Instructions** in Project Settings
2. Copy the certificate file path
3. Double-click the certificate file
4. Click **Install Certificate**
5. Select **Local Machine** → **Next**
6. Choose **Place all certificates in the following store**
7. Click **Browse** → Select **Trusted Root Certification Authorities**
8. Click **Next** → **Finish**
9. Restart your browser

### macOS

1. Click **View Trust Instructions** in Project Settings
2. Copy the certificate file path
3. Open **Keychain Access** app
4. Drag the certificate file into **System** keychain
5. Find the certificate (search for "API Dev Studio")
6. Double-click → Expand **Trust** section
7. Set **When using this certificate** to **Always Trust**
8. Close and enter your password
9. Restart your browser

### Linux

1. Click **View Trust Instructions** in Project Settings
2. Copy the certificate file path
3. Copy certificate to system trust store:
   ```bash
   sudo cp /path/to/cert.pem /usr/local/share/ca-certificates/apidevstudio.crt
   sudo update-ca-certificates
   ```
4. For Firefox: Import certificate in Settings → Privacy & Security → Certificates → View Certificates → Import

## Certificate Details

Each project gets its own self-signed certificate:

- **Algorithm**: RSA 2048-bit
- **Valid for**: 365 days from generation
- **Common Name**: `localhost`
- **Subject Alternative Names**: `localhost`, `127.0.0.1`, `::1`

View certificate details in **Project Settings**:
- Fingerprint (SHA-256)
- Expiration date
- File location

## Auto-Renewal

Certificates are valid for 1 year. API Dev Studio will warn you when a certificate is about to expire. To renew:

1. Open **Project Settings**
2. Toggle **Enable HTTPS** off
3. Toggle **Enable HTTPS** on
4. A new certificate is generated
5. Re-trust the new certificate following the steps above

## Deleting Certificates

To remove a project's certificate:

1. Open **Project Settings**
2. Toggle **Enable HTTPS** off
3. Click **Delete Certificate** (if shown)

Certificate files are stored in: `%APPDATA%\api-dev-studio\projects\{project-id}\certs\`

## Testing HTTPS Endpoints

### Using Browser

Visit `https://localhost:{port}/your-endpoint` directly. If you've trusted the certificate, you won't see any warnings.

### Using cURL

```bash
# Trust the certificate
curl https://localhost:3001/api/users

# Or skip verification (not recommended)
curl -k https://localhost:3001/api/users
```

### Using Postman

1. Go to Settings → Certificates
2. Click **Add Certificate**
3. Set **Host**: `localhost:{port}`
4. Select the certificate file from Project Settings
5. Enable the certificate

## Troubleshooting

### "NET::ERR_CERT_AUTHORITY_INVALID" in browser

The certificate hasn't been trusted yet. Follow the trust instructions for your OS above.

### "curl: (60) SSL certificate problem"

Either trust the certificate system-wide, or use `curl -k` to skip verification (for testing only).

### Certificate expired

Certificates are valid for 1 year. Generate a new certificate by toggling HTTPS off and back on.

### Can't find certificate file

1. Open **Project Settings**
2. Certificate path is shown under "Certificate Status"
3. Copy the path and open it in File Explorer

## Security Notes

- **Development only**: Self-signed certificates are for local development only
- **Not for production**: Use a real certificate (Let's Encrypt, etc.) for production
- **Don't share certificates**: Each project should have its own certificate
- **Trust implications**: Trusting a certificate means your system will accept it as valid
