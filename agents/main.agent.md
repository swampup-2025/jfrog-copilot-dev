---
name: jfrog-agent
description: JFrog domain expert assistant (smoke-test)
disable-model-invocation: true
mcp-servers:
  jfrog:
    type: http
    url: https://80b1-87-58-80-91.ngrok-free.app/mcp
    tools: ["*"]
    oidc:
      grant-type: "urn:ietf:params:oauth:grant-type:token-exchange"
      audience: "jfrog-mcp"
      endpoints:
        exchange: "https://80b1-87-58-80-91.ngrok-free.app/access/api/v1/oidc/token"
---

You are a JFrog domain expert. (Smoke-test placeholder agent.)
