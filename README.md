# jfrog-copilot-dev

Development / smoke-test version of the JFrog plugin for GitHub Copilot (AgentHQ).

## Purpose

This repo is a minimal scaffold used to smoke-test GitHub Copilot's OIDC token-exchange flow against a locally running JFrog Access service.

## Structure

- `plugin.json` -- plugin manifest
- `agents/main.agent.md` -- main agent with MCP server + OIDC config

## OIDC flow (token-exchange)

GitHub Copilot exchanges its short-lived OIDC JWT for a JFrog access token via RFC 8693 token-exchange against the central-integration MCP gateway at `https://central-integration.jfrog.io/mcp`.

No explicit `oidc.endpoints.exchange` is configured -- Copilot discovers the exchange endpoint via the MCP server's `oauth-authorization-server` metadata at `https://central-integration.jfrog.io/.well-known/oauth-authorization-server`.

## Tenant routing

Because the MCP URL is shared across all customers, per-tenant routing is driven by the `X-JFrog-Tenant-Id` header. The plugin sets it from a customer-supplied GitHub secret using GitHub's `${COPILOT_MCP_*}` interpolation:

```yaml
headers:
  X-JFrog-Tenant-Id: ${COPILOT_MCP_JFROG_TENANT_ID}
```

The `headers` block applies to both the OIDC token-exchange request and subsequent MCP traffic.

### Customer setup (one-time, manual)

Each customer must create the secret in their GitHub org:

1. GitHub org -> Settings -> Secrets and variables -> Agents
2. New secret: `COPILOT_MCP_JFROG_TENANT_ID`
3. Value: their JFrog tenant id (e.g. `mycompany`)

Without this secret the header arrives empty and routing fails.

## Status

Pre-MVP / experimental. Not for customer use.

## License

Apache 2.0
