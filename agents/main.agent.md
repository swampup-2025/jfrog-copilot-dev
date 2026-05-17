---
name: jfrog-agent
description: JFrog domain expert assistant (smoke-test)
disable-model-invocation: true
mcp-servers:
  jfrog:
    type: http
    url: https://${COPILOT_MCP_JFROG_HOST}/mcp
    tools: ["*"]
    oidc:
      grant-type: "urn:ietf:params:oauth:grant-type:token-exchange"
      audience: "jfrog-mcp"
---

You are a JFrog domain expert. (Smoke-test placeholder agent.)
