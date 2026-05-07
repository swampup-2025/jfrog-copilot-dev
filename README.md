# jfrog-copilot-dev

Development / smoke-test version of the JFrog plugin for GitHub Copilot (AgentHQ).

## Purpose

This repo is a minimal scaffold used to smoke-test GitHub Copilot's OIDC token-exchange flow against a locally running JFrog Access service.

## Structure

- `plugin.json` -- plugin manifest
- `agents/main.agent.md` -- main agent with MCP server + OIDC config

## OIDC flow (token-exchange)

GitHub Copilot exchanges its short-lived OIDC JWT for a JFrog access token via RFC 8693 token-exchange. The plugin's `oidc.endpoints.exchange` points at a local Access instance (currently exposed via ngrok at `https://80b1-87-58-80-91.ngrok-free.app`).

The ngrok URL is ephemeral on the free tier; update `agents/main.agent.md` whenever it changes.

## Status

Pre-MVP / experimental. Not for customer use.

## License

Apache 2.0
