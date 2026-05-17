# jfrog-copilot-dev

Development / smoke-test version of the JFrog plugin for GitHub Copilot (AgentHQ).

## Purpose

This repo is a minimal scaffold used to smoke-test GitHub Copilot's OIDC token-exchange flow against a JFrog Platform Deployment (JPD).

## Structure

- `plugin.json` -- plugin manifest
- `agents/main.agent.md` -- main agent with MCP server + OIDC config

## MCP URL

Each customer points the plugin at their own JPD via a single GitHub secret. The agent file uses Copilot's `${COPILOT_MCP_*}` interpolation directly in the `url:` field:

```yaml
mcp-servers:
  jfrog:
    type: http
    url: https://${COPILOT_MCP_JFROG_HOST}/mcp
```

At runtime Copilot resolves `${COPILOT_MCP_JFROG_HOST}` from the customer's GitHub org secrets, so each tenant connects to its own JPD with no shared routing layer.

## OIDC flow (token-exchange)

GitHub Copilot exchanges its short-lived OIDC JWT for a JFrog access token via RFC 8693 token-exchange against the customer's own JPD. No explicit `oidc.endpoints.exchange` is configured -- Copilot discovers the exchange endpoint via the MCP server's `oauth-authorization-server` metadata at `https://<their-host>/.well-known/oauth-authorization-server`.

## Customer setup (one-time, manual)

Each customer must create the secret in their GitHub org:

1. GitHub org -> Settings -> Secrets and variables -> Agents
2. New secret: `COPILOT_MCP_JFROG_HOST`
3. Value: their JPD hostname (e.g. `productdemo.jfrog.io`)

Without this secret the URL resolves to `https:///mcp` and the handshake fails.

## Status

Pre-MVP / experimental. Not for customer use.

## License

Apache 2.0
