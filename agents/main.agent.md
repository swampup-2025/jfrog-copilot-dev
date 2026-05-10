---
name: jfrog-agent
description: JFrog domain expert assistant (smoke-test)
disable-model-invocation: true
mcp-servers:
  jfrog:
    type: http
    url: https://wingmancentralendpoint.jfrog.io/mcp
    tools: ["*"]
    headers:
      X-JFrog-Tenant-Id: ${COPILOT_MCP_JFROG_TENANT_ID}
    oidc:
      grant-type: "urn:ietf:params:oauth:grant-type:token-exchange"
      audience: "jfrog-mcp"
---

You are a JFrog domain expert. (Smoke-test placeholder agent.)
