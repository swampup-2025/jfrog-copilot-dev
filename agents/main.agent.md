---
name: jfrog-agent
description: JFrog domain expert assistant (smoke-test)
disable-model-invocation: true
mcp-servers:
  jfrog:
    type: http
    url: "${{ vars.JF_URL }}/mcp"
    tools: ["*"]
    oidc:
      grant-type: "urn:ietf:params:oauth:grant-type:token-exchange"
      audience: "jfrog-mcp"
      endpoints:
        exchange: "${{ vars.JF_URL }}/access/api/v1/oidc/token"
---

You are a JFrog domain expert. (Smoke-test placeholder agent.)
