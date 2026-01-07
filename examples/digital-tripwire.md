---
description: >-
  Configure high-fidelity alerts for specific commands using the Digital Tripwire system.
icon: bell
---

# Digital Tripwire

The Digital Tripwire system allows you to tag specific interactions as high-priority alerts with configurable severity levels. This is useful for detecting high-signal indicators of compromise (IoCs) amidst the noise of automated scanners.

### Configuration Fields

- `alert`: Set to `true` to mark the interaction as an alert.
- `severity`: The severity level of the alert. Options: `medium` (default), `high`, `critical`.

### Example

Here is a configuration that simulates a Linux server where accessing sensitive files or attempting outbound connections triggers alerts.

```yaml
apiVersion: "v1"
protocol: "ssh"
address: ":2222"
description: "SSH Tripwire Configuration"
commands:
  # Normal interaction - Logged but not alerted
  - regex: "^ls$"
    handler: "Documents Downloads Pictures"

  # Suspicious activity - High severity alert
  - regex: "^(curl|wget) .*$"
    handler: "command not found"
    alert: true
    severity: "high"

  # Critical security event - Critical severity alert
  - regex: "^cat /etc/shadow$"
    handler: "Permission denied"
    alert: true
    severity: "critical"
```
