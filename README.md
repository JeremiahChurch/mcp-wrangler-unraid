# MCP Wrangler - Unraid Template

Docker template for installing [MCP Wrangler](https://github.com/JeremiahChurch/mcp-wrangler) on Unraid via Community Applications.

## Manual Installation (before CA approval)

1. In the Unraid web UI, go to **Docker** > **Add Container**
2. Click **Template Repositories** at the bottom
3. Add this URL: `https://github.com/JeremiahChurch/mcp-wrangler-unraid`
4. Click **Save**
5. Go back to **Add Container** and select **mcp-wrangler** from the template dropdown
6. Fill in the required fields (encryption key, session secret, admin password)
7. Click **Apply**

## Configuration

| Field | Required | Description |
|---|---|---|
| Web UI Port | Yes | Default: 8080 |
| Data Directory | Yes | Persistent storage for SQLite DB. Default: `/mnt/user/appdata/mcp-wrangler` |
| Docker Socket | Yes | Required for managing stdio/HTTP MCP server containers |
| Encryption Key | Yes | Encrypts stored credentials. Generate with `openssl rand -hex 32` |
| Session Secret | Yes | Signs session cookies. Generate with `openssl rand -hex 32` |
| Admin Password | Yes | Initial admin password (first run only) |
| Base URL | No | Set if using a reverse proxy (e.g., `https://mcp.yourdomain.com`) |

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
