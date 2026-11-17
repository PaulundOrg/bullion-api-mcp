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
gold data and macro data. Its default scopes include `portfolio:read`, so a default
connection can also read the signed-in user's own portfolio, lots, gains and
transactions. It has no trade, payment or portfolio-changing tool.

## Steps

1. Add a remote MCP server to the client's MCP settings with the type
   `streamable-http` (Streamable HTTP) and the URL above. Name it `bullion-api`.
2. Start the connection. The client opens a browser sign-in page at Bullion API.
3. The user signs in and, on the consent screen, approves read-only access with the
   "Allow read-only access" button, or declines. If the client also asks for
   `offline_access`, the screen lists "Stay connected"
   among the requested access; approving it lets the client renew its access
   without signing in again. Each renewal starts a new 30-day window, so a client
   that renews at least every 30 days stays connected.
4. When the connection is ready, the client lists the server's tools. Read-only
   tools such as `get_metal_price` and `get_metal_price_history` should appear.
5. Check the result with one read-only call, for example the latest gold price in
   USD. Report the value with its observation date, because the data is a dated
   observation and not a live quote.

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
