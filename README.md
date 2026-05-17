# jfrog-copilot-dev

Development / smoke-test version of the JFrog plugin for GitHub Copilot (AgentHQ).

## Purpose

This repo is a minimal scaffold used to smoke-test GitHub Copilot's OIDC token-exchange flow against a JFrog Platform Deployment (JPD).

## Structure

- `plugin.json` -- plugin manifest
- `agents/main.agent.md` -- main agent with MCP server + OIDC config

## MCP URL

Each customer points the plugin at their own JPD via a single GitHub variable. The agent file uses Copilot's `${COPILOT_MCP_*}` interpolation directly in the `url:` field:

```yaml
mcp-servers:
  jfrog:
    type: http
    url: ${COPILOT_MCP_JFROG_URL}/mcp
```

At runtime Copilot resolves `${COPILOT_MCP_JFROG_URL}` from the customer's GitHub Agents variables, so each tenant connects to its own JPD with no shared routing layer.

## OIDC flow (token-exchange)

GitHub Copilot exchanges its short-lived OIDC JWT for a JFrog access token via RFC 8693 token-exchange against the customer's own JPD. No explicit `oidc.endpoints.exchange` is configured -- Copilot discovers the exchange endpoint via the MCP server's `oauth-authorization-server` metadata at `<their-url>/.well-known/oauth-authorization-server`.

## Customer setup (one-time, manual)

Each customer must create the variable in their GitHub org or repo:

1. GitHub org/repo -> Settings -> Secrets and variables -> Agents -> Variables
2. New variable: `COPILOT_MCP_JFROG_URL`
3. Value: their JPD base URL, including scheme (e.g. `https://productdemo.jfrog.io`)

Without this variable the URL resolves to `/mcp` and the handshake fails.

## Status

Pre-MVP / experimental. Not for customer use.

## License

Apache 2.0
