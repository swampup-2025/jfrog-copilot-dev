# jfrog-copilot-dev

Development / smoke-test version of the JFrog plugin for GitHub Copilot (AgentHQ).

## Purpose

This repo is a minimal scaffold used to smoke-test GitHub Copilot's OIDC token-exchange flow against a locally running JFrog Access service.

## Structure

- `plugin.json` -- plugin manifest
- `agents/main.agent.md` -- main agent with MCP server + OIDC config

## OIDC flow (token-exchange)

GitHub Copilot exchanges its short-lived OIDC JWT for a JFrog access token via RFC 8693 token-exchange. The plugin's `oidc.endpoints.exchange` points at the JFrog instance configured via the `JF_URL` Agentic App variable.

## Configuration

The plugin uses GitHub Actions-style variable substitution to keep the JFrog URL out of the source. Set the `JF_URL` variable on the Agentic App config (e.g., `https://your-tenant.jfrog.io` or an ngrok URL for local testing). The `agents/main.agent.md` file references it as `${{ vars.JF_URL }}` for both the MCP server URL and the OIDC token-exchange endpoint.

Note: variable-substitution support in `.mcp.json` is being verified with GitHub. If unsupported, the URL must be hardcoded -- see commit history for the previous explicit-URL version.

## Status

Pre-MVP / experimental. Not for customer use.

## License

Apache 2.0
