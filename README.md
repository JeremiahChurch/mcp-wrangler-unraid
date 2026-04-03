# Arc Relay - Unraid Template

Docker template for installing [Arc Relay](https://github.com/comma-compliance/arc-relay) (formerly MCP Wrangler) on Unraid via Community Applications.

## Manual Installation (before CA approval)

1. In the Unraid web UI, go to **Docker** > **Add Container**
2. Click **Template Repositories** at the bottom
3. Add this URL: `https://github.com/JeremiahChurch/mcp-wrangler-unraid`
4. Click **Save**
5. Go back to **Add Container** and select **arc-relay** from the template dropdown
6. Fill in the required fields (encryption key, admin password)
7. Click **Apply**

## Upgrading from MCP Wrangler

If you have an existing MCP Wrangler installation:

1. Note your current encryption key (from the container env vars)
2. Remove the old `mcp-wrangler` container
3. Install `arc-relay` from the template
4. Set the **Data Directory** to your existing path (`/mnt/user/appdata/mcp-wrangler`)
5. Use the **same encryption key** - without it, your encrypted configs are unreadable
6. Either rename your DB file from `mcp-wrangler.db` to `arc-relay.db`, or set **Database Path** to `/data/mcp-wrangler.db`

## Configuration

| Field | Required | Description |
|---|---|---|
| Web UI Port | Yes | Default: 8080 |
| Data Directory | Yes | Persistent storage for SQLite DB. Default: `/mnt/user/appdata/arc-relay` |
| Docker Socket | Yes | Required for managing stdio/HTTP MCP server containers |
| Encryption Key | Yes | Encrypts stored credentials. Generate with `openssl rand -hex 32` |
| Session Secret | No | Signs session cookies. Generate with `openssl rand -hex 32` |
| Admin Password | Yes | Initial admin password (first run only) |
| Base URL | No | Set if using a reverse proxy (e.g., `https://mcp.yourdomain.com`) |
| Sentry DSN | No | Sentry error tracking DSN (advanced) |

## After Installation

1. Open the web UI at `http://your-unraid-ip:8080`
2. Log in with `admin` and the password you set
3. Add MCP servers via the dashboard
4. Generate API keys under **API Keys**
5. Point your AI tools at the proxy:
   ```
   claude mcp add --transport http my-server \
     http://your-unraid-ip:8080/mcp/my-server \
     --header "Authorization: Bearer YOUR_API_KEY"
   ```
