---
description: Take your first steps with the Beelzebub Framework.
icon: bullseye-arrow
---

# Quickstart

The Beelzebub Framework provides a simple yaml interface to configure a honeypot. This example configure a simple SSH honeypot.&#x20;

```yaml
apiVersion: "v1"
protocol: "ssh"
address: ":22"
description: "SSH simple honeypot"
commands:
  - regex: "^ls$"
    handler: "Documents Images  Desktop Downloads .m2 .kube .ssh  .docker"
  - regex: "^pwd$"
    handler: "/home/"
  - regex: "^uname -m$"
    handler: "x86_64"
   - regex: "^docker .*$"
    handler: "Error response from daemon: dial unix docker.raw.sock: connect: connection refused"
  - regex: "^uname$"
    handler: "Linux"
  - regex: "^(.+)$"
    handler: "command not found"
serverVersion: "OpenSSH"
serverName: "ubuntu"
passwordRegex: "^(root|qwerty|Smoker666|123456|jenkins|minecraft|sinus|alex|postgres|Ly123456)$"
deadlineTimeoutSeconds: 60
```

### Run Beelzebub

We provide two quick start options for run Beelzebub: using Go compiler or docker container.

### Go compiler

```bash
git clone https://github.com/mariocandela/beelzebub.git
go mod download
go build
./beelzebub
```

### Docker compose

```bash
git clone https://github.com/mariocandela/beelzebub.git
docker compose build
docker-compose up -d
```

You can find the precompiled container at the following link: [https://hub.docker.com/r/m4r10/beelzebub](https://hub.docker.com/r/m4r10/beelzebub)

Now that you have executed Beelzebub, you will find several pre-configured honeypots within the project. They are located inside the `configurations/services` directory, try the simple SSH honeypot on port 22

```bash
ssh root@localhost
```

{% hint style="info" %}
Password: root&#x20;
{% endhint %}
