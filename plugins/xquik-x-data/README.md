# Xquik X Data Plugin

Use Xquik from Claude Code for X data workflows through the documented REST API and remote MCP endpoint.

## What It Helps With

- Set up the Xquik remote MCP server.
- Plan REST API calls with the current OpenAPI spec.
- Search, export, monitor, and receive webhook events for X data.
- Keep write or persistent workflows behind explicit user approval.

## Setup

Set an API key before using the plugin:

```bash
export XQUIK_API_KEY="your-api-key"
```

Add the marketplace, then install the plugin:

```text
/plugin marketplace add tasanakorn/cc-marketplace
/plugin install xquik-x-data
```

## Sources

- Docs: https://docs.xquik.com
- OpenAPI: https://xquik.com/openapi.json
- MCP manifest: https://xquik.com/.well-known/mcp.json
- Source: https://github.com/Xquik-dev/x-twitter-scraper

## License

MIT
