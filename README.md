# Stalwart Mail Server on Dokploy

This repository contains the configuration to deploy [Stalwart Mail Server](https://stalw.art/) using Docker on Dokploy.

## DNS Configuration (Crucial for Subdomain)

To use a subdomain (e.g., `mail.yourdomain.com`), add these records in your DNS provider:

| Type | Name | Value | Priority |
| :--- | :--- | :--- | :--- |
| **A** | `mail` | `YOUR_VPS_IP` | - |
| **MX** | `mail` | `mail.yourdomain.com.` | `10` |
| **TXT** | `mail` | `v=spf1 a -all` | - |

> [!NOTE]
> Replace `mail` with your preferred subdomain name.

## Deployment Steps

1. **GitHub Setup**: 
   - Push this repository to your GitHub account (already linked as `git@github.com:SE2-Coder/instant-stalwart-docker.git`).

2. **Dokploy Configuration**:
   - Go to your Dokploy Dashboard.
   - Create a new **Compose** deployment.
   - Point it to this repository.
   - **Environment Variables**: Add `STALWART_ADMIN_PASSWORD` in Dokploy with the password found in your `AccessStalwart.sql` file.

3. **Firewall Setup**:
   Ensure the following ports are open on your VPS (YOUR_VPS_IP):
   - `25` (SMTP)
   - `465` (SMTPS)
   - `587` (Submission)
   - `143` (IMAP)
   - `993` (IMAPS)
   - `8080` (HTTP Admin UI)

4. **Initial Access**:
   Once deployed, access the admin interface at `http://<your-ip>:8080` or configure a domain in Dokploy settings.

## Security Note

The `AccessStalwart.sql` file and SSH keys are excluded via `.gitignore` and must **never** be committed to this repository.
