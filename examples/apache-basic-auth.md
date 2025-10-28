---
description: >-
  In this configuration, an example of how to replicate an Apache server
  protected by basic auth.
icon: server
---

# Apache basic auth

```yaml
apiVersion: "v1"
protocol: "http"
address: ":8080"
description: "Apache 401"
commands:
  - regex: ".*"
    handler: "Unauthorized"
    headers:
      - "www-Authenticate: Basic"
      - "server: Apache"
    statusCode: 401
```
