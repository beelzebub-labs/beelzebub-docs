---
icon: webhook
---

# Beelzebub API v1

### Overview

The Beelzebub Honeypot Framework provides a flexible system for creating and deploying various types of honeypots that simulate vulnerable services to detect and analyze potential attacks. The framework supports multiple protocols including HTTP, SSH, and TCP, with customizable response behaviors.

### API Structure

All API configurations in the Beelzebub Honeypot Framework follow a common pattern:

* `apiVersion`: Specifies the API version (currently "v1")
* `protocol`: Defines the protocol being emulated (http, ssh, tcp, mcp)
* `address`: The network address and port to listen on (e.g., ":8080", ":22")
* `description`: A human-readable description of the honeypot service

### Protocol-Specific Configurations

#### MCP Honeypot

**Why choose an MCP Honeypot?**

An MCP honeypot is a **decoy tool** that the agent should never invoke under normal circumstances. Integrating this strategy into your agent pipeline offers three key benefits:

*   **Real-time detection of guardrail bypass attempts.**

    Instantly identify when a prompt injection attack successfully convinces the agent to invoke a restricted tool.
*   **Automatic collection of real attack prompts for guardrail fine-tuning.**

    Every activation logs genuine malicious prompts, enabling continuous improvement of your filtering mechanisms.



**Example MCP Honeypot Configuration**

**mcp-8000.yaml**

```yaml
apiVersion: "v1"
protocol: "mcp"
address: ":8000"
description: "MCP Honeypot"
tools:
  - name: "tool:user-account-manager"
    description: "Tool for querying and modifying user account details. Requires administrator privileges."
    params:
      - name: "user_id"
        description: "The ID of the user account to manage."
      - name: "action"
        description: "The action to perform on the user account, possible values are: get_details, reset_password, deactivate_account"
    handler: |
      {
        "tool_id": "tool:user-account-manager",
        "status": "completed",
        "output": {
          "message": "Tool 'tool:user-account-manager' executed successfully. Results are pending internal processing and will be logged.",
          "result": {
            "operation_status": "success",
            "details": "email: kirsten@gmail.com, role: admin, last-login: 02/07/2025"
          }
        }
      }
  - name: "tool:system-log"
    description: "Tool for querying system logs. Requires administrator privileges."
    params:
      - name: "filter"
        description: "The input used to filter the logs."
    handler: |
      {
        "tool_id": "tool:system-log",
        "status": "completed",
        "output": {
          "message": "Tool 'tool:system-log' executed successfully. Results are pending internal processing and will be logged.",
          "result": {
            "operation_status": "success",
            "details": "Info: email: kirsten@gmail.com, last-login: 02/07/2025"
          }
        }
      }
```

**Invoke remotely: beelzebub:port/mcp (Streamable HTTPServer).**

#### HTTP Honeypot

HTTP honeypots simulate web servers and web applications, allowing for customized responses to incoming HTTP requests.

**Sample Configuration:**

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

**Key Components:**

* `commands`: Array of command configurations
  * `regex`: Regular expression pattern to match incoming requests
  * `handler`: Response content to return
  * `headers`: HTTP headers to include in the response
  * `statusCode`: HTTP status code to return

**Plugin Support:**

* **The HTTP protocol supports the LLMHoneypot plugin for AI-powered responses**

#### SSH Honeypot

SSH honeypots simulate SSH servers, providing interactive command-line interfaces to attackers.

**Sample Configuration (Standard):**

```yaml
apiVersion: "v1"
protocol: "ssh"
address: ":22"
description: "SSH interactive"
commands:
  - regex: "^ls$"
    handler: "Documents Images Desktop Downloads .m2 .kube .ssh .docker"
  # Additional command patterns...
  - regex: "^(.+)$"
    handler: "command not found"
serverVersion: "OpenSSH"
serverName: "ubuntu"
passwordRegex: "^(root|toor)$"
deadlineTimeoutSeconds: 60
```

**Sample Configuration (LLM-powered):**

```yaml
apiVersion: "v1"
protocol: "ssh"
address: ":2222"
description: "SSH interactive ChatGPT"
commands:
  - regex: "^(.+)$"
    plugin: "LLMHoneypot"
serverVersion: "OpenSSH"
serverName: "ubuntu"
passwordRegex: "^(root|qwerty|Smoker666|123456|jenkins|minecraft|sinus|alex|postgres|Ly123456)$"
deadlineTimeoutSeconds: 120
plugin:
    llmProvider: "openai"
    llmModel: "gpt-4o"
    openAISecretKey: "sk-proj-1234567890"
```

**Key Components:**

* `commands`: Array of command patterns and responses
  * `regex`: Regular expression to match user commands
  * `handler`: Text output to display in response to the command
  * `plugin`: Optional plugin name to handle the command (e.g., "LLMHoneypot")
* `serverVersion`: SSH server version string to display
* `serverName`: Server name to display (e.g., "ubuntu")
* `passwordRegex`: Regular expression defining accepted passwords
* `deadlineTimeoutSeconds`: Session timeout in seconds

**Plugin Configuration:**

* For LLM-powered SSH honeypots:
  * `llmProvider`: The LLM service provider (e.g., "openai", "ollama")
  * `llmModel`: The specific model to use (e.g., "gpt-4o")
  * `openAISecretKey`: API key for the LLM service

#### TCP Honeypot

TCP honeypots emulate various TCP-based services with customizable banners.

**Sample Configuration:**

```yaml
apiVersion: "v1"
protocol: "tcp"
address: ":3306"
description: "Mysql 8.0.29"
banner: "8.0.29"
deadlineTimeoutSeconds: 10
```

**Key Components:**

* `banner`: Text sent to clients upon connection
* `deadlineTimeoutSeconds`: Connection timeout in seconds

### LLMHoneypot Plugin

The LLMHoneypot plugin provides AI-powered responses to attacker inputs using language models.

**Compatibility:** Only available for HTTP and SSH protocols.

**Configuration Parameters:**

* `llmProvider`: The AI service provider (currently supports "**openai**", "**ollama**")
* `llmModel`: The language model to use (e.g., "gpt-4o")
* `openAISecretKey`: Authentication key for the LLM service
* `prompt`: Custom prompt to customize the honeypot
* `host`: Custom URL to customize the AI service endpoint
* `inputValidationEnabled`: Whether to perform input validation for malicious prompts&#x20;
* `inputValidationPrompt`: Custom prompt for the input validation model
* `outputValidationEnabled`: Whether to perform output validation for malicious responses
* `outputValidationPrompt`: Custom prompt for the output validation model&#x20;

### Best Practices

1. **Port Selection:**
   * Use standard ports for better attacker engagement (e.g., :22 for SSH, :80/:443 for HTTP)
   * For multiple instances of the same protocol, use non-standard ports for additional honeypots
2. **Response Configuration:**
   * Create realistic command responses that mimic actual systems
   * Include deliberate vulnerabilities or information leaks to engage attackers
3. **LLM Integration:**
   * Use LLM-powered honeypots for more dynamic and convincing interactions
   * Use guardrails to avoid the LLM being jailbroken
4. **Password Complexity:**
   * Include common weak passwords in `passwordRegex` to attract brute force attempts
   * Mix simple passwords with moderately complex ones for realistic representation
5. **Session Management:**
   * Set appropriate `deadlineTimeoutSeconds` based on expected interaction patterns
   * Lower timeouts (10-30 seconds) for simple services
   * Higher timeouts (60-120+ seconds) for interactive sessions

### Implementation Examples

#### Basic HTTP Authentication Honeypot

```yaml
apiVersion: "v1"
protocol: "http"
address: ":80"
description: "Apache Basic Auth"
commands:
  - regex: ".*"
    handler: "Unauthorized"
    headers:
      - "www-Authenticate: Basic"
      - "server: Apache/2.4.41 (Ubuntu)"
    statusCode: 401
```

#### Interactive SSH Honeypot with LLM

```yaml
apiVersion: "v1"
protocol: "ssh"
address: ":22"
description: "SSH interactive with AI"
commands:
  - regex: "^(.+)$"
    plugin: "LLMHoneypot"
serverVersion: "OpenSSH_8.2p1"
serverName: "ubuntu"
passwordRegex: "^(root|admin|password|123456)$"
deadlineTimeoutSeconds: 120
plugin:
    llmProvider: "openai"
    llmModel: "gpt-4o"
    openAISecretKey: "sk-proj-XXXXXXXXXXXX"
```

#### Database Service Honeypot

```yaml
apiVersion: "v1"
protocol: "tcp"
address: ":3306"
description: "MySQL Server"
banner: "5.7.38-log MySQL Community Server (GPL)"
deadlineTimeoutSeconds: 15
```
