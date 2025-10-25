---
description: 'Follow a SSH LLM Honeypot using OpenAI as provider LLM:'
icon: microchip-ai
---

# SSH LLM Honeypot

Using LLM plugin AI acts as a Linux terminal and works as a high-interaction honeypot. However, it operates as a low-interaction honeypot, providing enhanced security without requiring constant supervision.

```yaml
apiVersion: "v1"
protocol: "ssh"
address: ":2222"
description: "SSH LLM Honeypot OpenAI GPT-4o"
commands:
  - regex: "^(.+)$"
    plugin: "LLMHoneypot"
serverVersion: "OpenSSH"
serverName: "ubuntu"
passwordRegex: "^(root|qwerty|Smoker666|123456|jenkins|minecraft|sinus|alex|postgres|Ly123456)$"
deadlineTimeoutSeconds: 60
plugin:
   llmProvider: "openai"
   llmModel: "gpt-4o"
   openAISecretKey: "sk-proj-123456"
```

Add your OpenAI SecretKey, and enjoy with your honeypot.

```bash
ssh root@localhost -p 2222
```
