---
description: N8N beelzebub honeypot configuration
icon: rabbit-running
---

# N8N honeypot

```yaml
apiVersion: "v1"
protocol: "http"
address: ":5678"
description: "n8n - Honeypot"
 
commands:
  # ==========================================================================
  # ENDPOINT: GET /signin
  # ==========================================================================
  - regex: "^/signin$"
    handler: |
      <!DOCTYPE html>
      <html lang="en">
      <head>
        <meta charset="UTF-8">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <title>n8n - Sign In</title>
        <style>
          body { font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif; 
                 background: #f5f5f5; display: flex; justify-content: center; align-items: center; 
                 height: 100vh; margin: 0; }
          .container { background: white; padding: 40px; border-radius: 8px; box-shadow: 0 2px 10px rgba(0,0,0,0.1); width: 360px; }
          .logo { text-align: center; margin-bottom: 30px; }
          .logo svg { width: 48px; height: 48px; }
          h1 { font-size: 24px; text-align: center; margin: 0 0 30px; color: #333; }
          input { width: 100%; padding: 12px; margin-bottom: 16px; border: 1px solid #ddd; 
                  border-radius: 4px; box-sizing: border-box; font-size: 14px; }
          button { width: 100%; padding: 12px; background: #ff6d5a; color: white; border: none; 
                   border-radius: 4px; cursor: pointer; font-size: 16px; font-weight: 600; }
          button:hover { background: #ff5a45; }
          .version { text-align: center; color: #999; font-size: 12px; margin-top: 20px; }
        </style>
      </head>
      <body>
        <div class="container">
          <div class="logo">
            <svg viewBox="0 0 100 100" fill="#ff6d5a"><circle cx="50" cy="50" r="45"/></svg>
          </div>
          <h1>Sign in to n8n</h1>
          <form action="/rest/login" method="post">
            <input type="email" name="email" placeholder="Email address" required>
            <input type="password" name="password" placeholder="Password" required>
            <button type="submit">Sign In</button>
          </form>
          <div class="version">n8n v1.120.0</div>
        </div>
      </body>
      </html>
    headers:
      - "Content-Type: text/html; charset=utf-8"
      - "Server: n8n"
      - "X-Powered-By: Express"
      - "X-n8n-Version: 1.120.0"
      - "Cache-Control: no-cache, no-store, must-revalidate"
    statusCode: 200
 
  # ==========================================================================
  # ENDPOINT: GET /rest/settings 
  # ==========================================================================
  - regex: "^/rest/settings$"
    handler: |
      {
        "data": {
          "n8nVersion": "1.120.0",
          "versionCli": "1.120.0",
          "databaseType": "sqlite",
          "authenticationMethod": "email",
          "defaultLocale": "en",
          "endpointWebhook": "webhook",
          "endpointWebhookTest": "webhook-test",
          "instanceId": "f8e7d6c5-b4a3-9281-7654-321fedcba098",
          "isDocker": true,
          "timezone": "Europe/Rome",
          "urlBaseWebhook": "https://n8n.example.com/",
          "urlBaseEditor": "https://n8n.example.com/",
          "executionMode": "regular",
          "pushBackend": "websocket",
          "communityNodesEnabled": true,
          "expressionEvaluator": "tmpl",
          "deployment": {
            "type": "default"
          },
          "enterprise": {
            "sharing": false,
            "ldap": false,
            "saml": false,
            "logStreaming": false,
            "advancedExecutionFilters": false,
            "variables": true,
            "sourceControl": false,
            "auditLogs": false,
            "externalSecrets": false,
            "workflowHistory": false
          },
          "security": {
            "blockFileAccessToN8nFiles": true,
            "restrictFileAccessTo": ""
          }
        }
      }
    headers:
      - "Content-Type: application/json; charset=utf-8"
      - "Server: n8n"
      - "X-Powered-By: Express"
      - "X-n8n-Version: 1.120.0"
      - "Cache-Control: no-cache"
    statusCode: 200
 
  # ==========================================================================
  # ENDPOINT: POST /rest/workflows
  # ==========================================================================
  - regex: "^/rest/workflows$"
    handler: |
      {
        "data": {
          "id": "wf_a1b2c3d4e5f67890",
          "name": "New Workflow",
          "active": false,
          "createdAt": "2025-12-25T12:00:00.000Z",
          "updatedAt": "2025-12-25T12:00:00.000Z",
          "versionId": "v1-a1b2c3d4",
          "nodes": [],
          "connections": {},
          "settings": {
            "saveExecutionProgress": true,
            "saveManualExecutions": true,
            "saveDataErrorExecution": "all",
            "saveDataSuccessExecution": "all",
            "executionTimeout": 3600,
            "timezone": "Europe/Rome"
          },
          "staticData": null,
          "tags": [],
          "sharedWith": []
        }
      }
    headers:
      - "Content-Type: application/json; charset=utf-8"
      - "Server: n8n"
      - "X-Powered-By: Express"
      - "X-n8n-Version: 1.120.0"
      - "X-Request-Id: req_f8e7d6c5b4a39281"
    statusCode: 201
 
  # ==========================================================================
  # ENDPOINT: PUT /rest/workflows/:id 
  # ==========================================================================
  - regex: "^/rest/workflows/[a-zA-Z0-9_-]+$"
    handler: |
      {
        "data": {
          "id": "wf_a1b2c3d4e5f67890",
          "name": "Updated Workflow",
          "active": false,
          "createdAt": "2025-12-20T10:30:00.000Z",
          "updatedAt": "2025-12-25T14:35:22.000Z",
          "versionId": "v2-b2c3d4e5",
          "nodes": [
            {
              "id": "start-node",
              "name": "Start",
              "type": "n8n-nodes-base.manualTrigger",
              "typeVersion": 1,
              "position": [100, 100],
              "parameters": {}
            }
          ],
          "connections": {},
          "settings": {
            "saveExecutionProgress": true,
            "saveManualExecutions": true
          }
        }
      }
    headers:
      - "Content-Type: application/json; charset=utf-8"
      - "Server: n8n"
      - "X-Powered-By: Express"
      - "X-n8n-Version: 1.120.0"
    statusCode: 200
 
  # ==========================================================================
  # ENDPOINT: POST /rest/workflows/:id/execute 
  # ==========================================================================
  - regex: "^/rest/workflows/[a-zA-Z0-9_-]+/execute$"
    handler: |
      {
        "data": {
          "executionId": "exec_9876543210fedcba",
          "mode": "manual",
          "startedAt": "2025-12-25T14:40:00.000Z",
          "status": "running",
          "workflowId": "wf_a1b2c3d4e5f67890",
          "workflowName": "Workflow",
          "data": {
            "resultData": {
              "runData": {},
              "lastNodeExecuted": "Start"
            }
          }
        }
      }
    headers:
      - "Content-Type: application/json; charset=utf-8"
      - "Server: n8n"
      - "X-Powered-By: Express"
      - "X-n8n-Version: 1.120.0"
      - "X-Execution-Id: exec_9876543210fedcba"
    statusCode: 200
 
  # ==========================================================================
  # ENDPOINT: GET /api/v1/workflows
  # ==========================================================================
  - regex: "^/api/v1/workflows$"
    handler: |
      {
        "data": [
          {
            "id": "wf_a1b2c3d4e5f67890",
            "name": "Production Workflow",
            "active": true,
            "createdAt": "2025-12-01T08:00:00.000Z",
            "updatedAt": "2025-12-24T16:30:00.000Z",
            "tags": [
              {
                "id": "tag_prod123",
                "name": "production"
              }
            ]
          },
          {
            "id": "wf_fedcba0987654321",
            "name": "Data Processing",
            "active": false,
            "createdAt": "2025-11-15T10:00:00.000Z",
            "updatedAt": "2025-12-20T12:00:00.000Z",
            "tags": []
          }
        ],
        "nextCursor": null
      }
    headers:
      - "Content-Type: application/json; charset=utf-8"
      - "Server: n8n"
      - "X-Powered-By: Express"
      - "X-n8n-Version: 1.120.0"
    statusCode: 200
 
  # ==========================================================================
  # ENDPOINT: /webhook/*
  # ==========================================================================
  - regex: "^/webhook/.*$"
    handler: |
      {
        "message": "Workflow was started",
        "executionId": "exec_webhook_1234567890",
        "success": true
      }
    headers:
      - "Content-Type: application/json; charset=utf-8"
      - "Server: n8n"
      - "X-Powered-By: Express"
      - "X-n8n-Version: 1.120.0"
      - "X-Webhook-Execution: exec_webhook_1234567890"
    statusCode: 200
 
  # ==========================================================================
  # ENDPOINT: /webhook-test/*
  # ==========================================================================
  - regex: "^/webhook-test/.*$"
    handler: |
      {
        "message": "Test webhook received",
        "mode": "test",
        "success": true
      }
    headers:
      - "Content-Type: application/json; charset=utf-8"
      - "Server: n8n"
      - "X-Powered-By: Express"
      - "X-n8n-Version: 1.120.0"
    statusCode: 200
 
  # ==========================================================================
  # ENDPOINT: POST /rest/login
  # ==========================================================================
  - regex: "^/rest/login$"
    handler: |
      {
        "data": {
          "user": {
            "id": "user_admin123",
            "email": "admin@n8n.local",
            "firstName": "Admin",
            "lastName": "User",
            "personalizationAnswers": null,
            "globalRole": {
              "id": "1",
              "name": "owner",
              "scope": "global"
            },
            "createdAt": "2025-01-01T00:00:00.000Z",
            "updatedAt": "2025-12-25T00:00:00.000Z",
            "settings": {
              "userActivated": true,
              "allowSSOManualLogin": true
            }
          }
        }
      }
    headers:
      - "Content-Type: application/json; charset=utf-8"
      - "Server: n8n"
      - "X-Powered-By: Express"
      - "X-n8n-Version: 1.120.0"
      - "Set-Cookie: n8n-auth=eyJhbGciOiJIUzI1NiJ9.eyJ1c2VySWQiOiJ1c2VyX2FkbWluMTIzIn0.fake_token; Path=/; HttpOnly; SameSite=Lax"
    statusCode: 200
 
  # ==========================================================================
  # ENDPOINT: GET /api/v1/credentials
  # ==========================================================================
  - regex: "^/api/v1/credentials$"
    handler: |
      {
        "data": [
          {
            "id": "cred_aws123",
            "name": "AWS Production",
            "type": "aws",
            "createdAt": "2025-06-01T10:00:00.000Z",
            "updatedAt": "2025-12-01T14:30:00.000Z"
          },
          {
            "id": "cred_db456",
            "name": "Database Connection",
            "type": "postgres",
            "createdAt": "2025-03-15T08:00:00.000Z",
            "updatedAt": "2025-11-20T16:00:00.000Z"
          },
          {
            "id": "cred_api789",
            "name": "Internal API Key",
            "type": "httpBasicAuth",
            "createdAt": "2025-09-10T12:00:00.000Z",
            "updatedAt": "2025-12-20T10:00:00.000Z"
          }
        ],
        "nextCursor": null
      }
    headers:
      - "Content-Type: application/json; charset=utf-8"
      - "Server: n8n"
      - "X-Powered-By: Express"
      - "X-n8n-Version: 1.120.0"
    statusCode: 200
 
  # ==========================================================================
  # ENDPOINT: GET /api/v1/executions
  # ==========================================================================
  - regex: "^/api/v1/executions.*$"
    handler: |
      {
        "data": [
          {
            "id": "exec_12345",
            "finished": true,
            "mode": "trigger",
            "retryOf": null,
            "startedAt": "2025-12-25T08:00:00.000Z",
            "stoppedAt": "2025-12-25T08:00:02.500Z",
            "workflowId": "wf_a1b2c3d4e5f67890",
            "status": "success"
          },
          {
            "id": "exec_12344",
            "finished": true,
            "mode": "manual",
            "retryOf": null,
            "startedAt": "2025-12-24T14:30:00.000Z",
            "stoppedAt": "2025-12-24T14:30:05.200Z",
            "workflowId": "wf_fedcba0987654321",
            "status": "error"
          }
        ],
        "nextCursor": null
      }
    headers:
      - "Content-Type: application/json; charset=utf-8"
      - "Server: n8n"
      - "X-Powered-By: Express"
      - "X-n8n-Version: 1.120.0"
    statusCode: 200
 
  - regex: "^/$"
    handler: |
      <!DOCTYPE html>
      <html><head><meta http-equiv="refresh" content="0;url=/signin"></head></html>
    headers:
      - "Content-Type: text/html; charset=utf-8"
      - "Server: n8n"
      - "X-Powered-By: Express"
      - "X-n8n-Version: 1.120.0"
    statusCode: 302
 
  - regex: "^/healthz?$"
    handler: |
      {
        "status": "ok"
      }
    headers:
      - "Content-Type: application/json; charset=utf-8"
      - "Server: n8n"
      - "X-Powered-By: Express"
    statusCode: 200
 
  - regex: "^.*$"
    handler: |
      {
        "code": 401,
        "message": "Unauthorized",
        "hint": "Missing or invalid API key. Set header 'X-N8N-API-KEY' or cookie 'n8n-auth'."
      }
    headers:
      - "Content-Type: application/json; charset=utf-8"
      - "Server: n8n"
      - "X-Powered-By: Express"
      - "X-n8n-Version: 1.120.0"
      - "WWW-Authenticate: Bearer realm=\"n8n\""
    statusCode: 401
```
