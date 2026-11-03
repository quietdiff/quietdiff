# QuietDiff

Low-noise web change monitoring with a hosted MCP server and REST API. https://quietdiff.com

Watch one part of a page (CSS selector) or one field of a JSON response (dot-path). Failed fetches and challenge pages are logged as check errors, not changes; a change is re-checked before it alerts. Checks are plain HTTP (no JavaScript rendering).

## Try it without signing up
```bash
curl -s -X POST https://quietdiff.com/api/demo/try-url \
  -H 'content-type: application/json' \
  -d '{"url":"https://example.com","selector":"h1"}'
```
Rate limited (5/min, 30/day per network).

## REST
```bash
curl https://quietdiff.com/api/v1/monitors \
  -H "Authorization: Bearer qd_YOUR_KEY" \
  -H 'content-type: application/json' \
  -d '{"url":"https://example.com/pricing","fields":[{"name":"price","selector":".price"}]}'
```
`X-API-Key: qd_...` also works. OpenAPI: https://quietdiff.com/openapi.json

## MCP (hosted, Streamable HTTP)
Endpoint `https://quietdiff.com/api/mcp`, header `Authorization: Bearer qd_YOUR_KEY`.

Cursor (`~/.cursor/mcp.json`) and other clients that take a remote URL:
```json
{ "mcpServers": { "quietdiff": { "url": "https://quietdiff.com/api/mcp",
  "headers": { "Authorization": "Bearer qd_YOUR_KEY" } } } }
```
Claude Desktop (via mcp-remote):
```json
{ "mcpServers": { "quietdiff": { "command": "npx",
  "args": ["-y","mcp-remote","https://quietdiff.com/api/mcp","--header","Authorization:Bearer qd_YOUR_KEY"] } } }
```
Claude Code: `claude mcp add --transport http quietdiff https://quietdiff.com/api/mcp --header "Authorization: Bearer qd_YOUR_KEY"`

Tools: `create_monitor`, `list_monitors`, `list_changes`, `get_snapshot`, `pause_monitor`, `get_monitor_health`.

## Plans (monthly)
Free 10 monitors daily · Starter $9 100 hourly · Pro $29 500 every 10 min · Agency $99 3,000 every 5 min.

Support: support@quietdiff.com
