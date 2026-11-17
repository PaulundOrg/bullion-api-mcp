# Install the Bullion API MCP server

This guide is for an AI agent that installs the Bullion API MCP server from this
repository. The server is hosted; nothing is cloned, built or run locally.

## What you are adding

- Server name: `bullion-api`
- Transport: Streamable HTTP
- URL: `https://api.bullionapi.dev/mcp`
- Authentication: OAuth 2.1 sign-in with PKCE. The client registers itself with
  dynamic client registration.
- Credentials: none in the configuration. Do not add an API key, a token or an
  `Authorization` header.

The server is read-only. It provides gold and precious-metal prices, central-bank
gold data and macro data. It has no trade, payment or portfolio-changing tool.

## Steps

1. Add a remote MCP server to the client's MCP settings with the type
   `streamable-http` (Streamable HTTP) and the URL above. Name it `bullion-api`.
2. Start the connection. The client opens a browser sign-in page at Bullion API.
3. The user signs in and approves read-only access on the consent screen. They
   can also approve "Stay connected", which lets the client renew its access
   without signing in again for up to 30 days.
4. When the connection is ready, the client lists the server's tools. Read-only
   tools such as `get_metal_price` and `get_metal_price_history` should appear.
5. Check the result with one read-only call, for example the latest gold price in
   USD. Report the value with its observation date, because the data is a dated
   observation and not a live quote.

## Claude Code

The pre-registered client can be used instead of dynamic registration:

```bash
claude mcp add --transport http --client-id bullion-claude-code-prod --callback-port 43829 bullion-api https://api.bullionapi.dev/mcp
```

## If something fails

- An unauthenticated request to the URL returns `401` with a pointer to the
  protected-resource metadata. This is expected before sign-in.
- If sign-in does not finish, start the connection again from the client's MCP
  settings.
- If tools are missing after sign-in, check that the consent screen was approved
  and reconnect.
- Never paste access tokens, refresh tokens, client secrets or API keys into a
  prompt or a configuration file.

Setup steps, permissions and API terms: <https://bullionapi.dev/docs/mcp> and
<https://bullionapi.dev/terms>.
