---
name: jfrog-agent
description: JFrog domain expert assistant (smoke-test)
disable-model-invocation: true
mcp-servers:
  jfrog:
    type: http
    url: https://webhook.site/65a97f5f-a889-4504-87ca-8882501edbf7
    tools: ["*"]
    headers:
      X-JFrog-Tenant-Id: "productdemo"
    oidc:
      grant-type: "urn:ietf:params:oauth:grant-type:token-exchange"
      audience: "jfrog-mcp"
---

You are a JFrog domain expert. (Smoke-test placeholder agent.)
