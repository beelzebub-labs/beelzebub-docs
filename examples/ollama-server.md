---
icon: rabbit-running
---

# Ollama server

```yaml
apiVersion: "v1"
protocol: "http"
address: ":11434"
description: "Ollama honeypot"
commands:
  - regex: "index"
    handler: "Ollama is running"
    headers:
      - "content-type: text/plain; charset=utf-8"
    statusCode: 200
  - regex: "api/tags"
    handler: "{\"models\":[{\"name\":\"llava:7b\",\"model\":\"llava:7b\",\"modified_at\":\"2025-02-26T10:32:23.1418245+08:00\",\"size\":4733363376,\"digest\":\"8dd30f6b0cb19f555f2c7a7ebda861449ea2cc76bf1f44e262931f45fc81d081\",\"details\":{\"parent_model\":\"\",\"format\":\"gguf\",\"family\":\"llama\",\"families\":[\"llama\",\"clip\"],\"parameter_size\":\"7B\",\"quantization_level\":\"Q4_0\"}}]}"
    headers:
      - "content-type: application/json; charset=utf-8"
    statusCode: 200
  - regex: ".*"
    handler: "404 page not found"
    headers:
      - "content-type: text/plain; charset=utf-8"
    statusCode: 404
```
