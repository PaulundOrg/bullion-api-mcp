# Bullion API plugin

Ask your agent about gold. This package connects an agent to the read-only Bullion API MCP server and adds market-analysis and portfolio-review skills. The root `plugin.json` and `mcp.json` use the Agent Plugins 1.0 schemas, `.claude-plugin/plugin.json` is the Claude Code manifest, and the skills use standard `SKILL.md` frontmatter.

## Connecting

The MCP server is `https://api.bullionapi.dev/mcp` over Streamable HTTP. Any MCP agent that supports OAuth 2.1 sign-in can add that URL: the agent registers itself, opens Bullion API in your browser, and you sign in and approve read-only access on the consent screen. In Claude Code you can also use the pre-registered client with `claude mcp add --transport http --client-id bullion-claude-code-prod --callback-port 43829 bullion-api https://api.bullionapi.dev/mcp`. Setup steps and permissions: <https://bullionapi.dev/docs/mcp>.

Never paste API keys, access tokens, client secrets, or other credentials into a prompt, and do not add credentials or authentication headers to this package.

Access tokens are valid for five minutes. When you approve "Stay connected" (`offline_access`) on the consent screen, the agent renews them with single-use refresh tokens for up to 30 days; otherwise, or after the connection lapses or consent is withdrawn, you reconnect through the agent's sign-in flow. Connecting, authentication and tool discovery are free; data calls use the same plans and limits as the REST API.

The plugin only guides read-only API calls; it contains no portfolio mutation workflow. Treat returned prices and statistics as dated observations, not real-time data. Preserve exact API decimal values for calculations and retain any public attribution required by a response. Review [API terms](https://bullionapi.dev/terms) for use and reuse restrictions.

## Optional local marketplace

The repository catalog at `.agents/plugins/marketplace.json` is an optional local authoring and discovery source. It does not auto-enable this plugin, register an external client, or publish anything.

Directory submissions are separate, explicit steps. OpenAI's review needs five positive and three negative test cases, a video walkthrough URL, and reviewer test-account details entered in its secure submission portal; Claude's plugin directory reads from a public repository. Keep reviewer credentials out of this package and prompts. Each listing must pass that directory's public review and approval.

## Submission preparation

Version 0.2.2 includes explicit OpenAI OAuth/DCR metadata and five positive and three
negative review scenarios. These describe expected behaviour; they are not recorded
passing results. The full operator pack is `docs/mcp-submission-pack.md` in the
application repository and must stay outside the uploaded plugin archive. It includes
ChatGPT, Claude and Muse intake copy, a demo script, local ZIP instructions and the
remaining operator inputs. No directory submission or publication is claimed.

The customer package is published at <https://github.com/PaulundOrg/bullion-api-mcp>.
Its configuration, assets and bundled skills are licensed under MIT; see `LICENSE`.
The Bullion API service and returned data remain subject to their separate terms.

## Product links

- Website: <https://bullionapi.dev>
- MCP documentation: <https://bullionapi.dev/docs/mcp>
- API documentation: <https://bullionapi.dev/docs>
- Support: <https://bullionapi.dev/contact>
- Privacy: <https://bullionapi.dev/privacy>
- Terms: <https://bullionapi.dev/terms>
