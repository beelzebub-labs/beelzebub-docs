---
description: >-
  This configuration was created by Akamai's hunt team, at the following link
  the original version:
icon: docker
---

# Docker API Honeypot

[https://github.com/akamai/Akamai-Hunt/blob/main/HoneypotConf/docker\_api\_honeypot\_conf.yaml](https://github.com/akamai/Akamai-Hunt/blob/main/HoneypotConf/docker_api_honeypot_conf.yaml)

```yaml
apiVersion: "v1"
protocol: "http"
address: ":2375"
description: "Docker Remote API honeypot (Docker/24.0.7 on linux, API 1.43, Linode host)"

commands:
  - regex: "^/_ping/?$"
    headers:
      - "Content-Type: text/plain; charset=utf-8"
      - "Server: Docker/24.0.7 (linux)"
      - "Api-Version: 1.43"
      - "Docker-Experimental: false"
      - "Ostype: linux"
    statusCode: 200
    handler: "OK"
  - regex: "^/v1\\.(\\d{2})/_ping/?$"
    headers:
      - "Content-Type: text/plain; charset=utf-8"
      - "Server: Docker/24.0.7 (linux)"
      - "Api-Version: 1.43"
      - "Docker-Experimental: false"
      - "Ostype: linux"
    statusCode: 200
    handler: "OK"

  - regex: "^/v1\\.(\\d{2})/version/?$"
    headers:
      - "Content-Type: application/json"
      - "Server: Docker/24.0.7 (linux)"
      - "Api-Version: 1.43"
      - "Docker-Experimental: false"
      - "Ostype: linux"
    statusCode: 200
    handler: |
      {
        "Platform": {"Name": "Docker Engine"},
        "Components": [
          {
            "Name": "Engine",
            "Version": "24.0.7",
            "Details": {
              "ApiVersion": "1.43",
              "MinAPIVersion": "1.12",
              "GitCommit": "b3e4c28f4dc06a09c1fa7a1ce3d2a8f1e9d741f6",
              "GoVersion": "go1.21.4",
              "Os": "linux",
              "Arch": "amd64",
              "BuildTime": "2024-11-12T10:30:00.000000000Z"
            }
          }
        ],
        "Version": "24.0.7",
        "ApiVersion": "1.43",
        "MinAPIVersion": "1.12",
        "GitCommit": "b3e4c28f4dc06a09c1fa7a1ce3d2a8f1e9d741f6",
        "GoVersion": "go1.21.4",
        "Os": "linux",
        "Arch": "amd64",
        "KernelVersion": "5.15.0-106-generic",
        "Experimental": false
      }

  - regex: "^/version/?$"
    headers:
      - "Content-Type: application/json"
      - "Server: Docker/24.0.7 (linux)"
      - "Api-Version: 1.43"
      - "Docker-Experimental: false"
      - "Ostype: linux"
    statusCode: 200
    handler: |
      {
        "Platform": {"Name": "Docker Engine"},
        "Components": [
          {
            "Name": "Engine",
            "Version": "24.0.7",
            "Details": {
              "ApiVersion": "1.43",
              "MinAPIVersion": "1.12",
              "GitCommit": "b3e4c28f4dc06a09c1fa7a1ce3d2a8f1e9d741f6",
              "GoVersion": "go1.21.4",
              "Os": "linux",
              "Arch": "amd64",
              "BuildTime": "2024-11-12T10:30:00.000000000Z"
            }
          }
        ],
        "Version": "24.0.7",
        "ApiVersion": "1.43",
        "MinAPIVersion": "1.12",
        "GitCommit": "b3e4c28f4dc06a09c1fa7a1ce3d2a8f1e9d741f6",
        "GoVersion": "go1.21.4",
        "Os": "linux",
        "Arch": "amd64",
        "KernelVersion": "5.15.0-106-generic",
        "Experimental": false
      }

  - regex: "^/info/?$"
    headers:
      - "Content-Type: application/json"
      - "Server: Docker/24.0.7 (linux)"
      - "Api-Version: 1.43"
    statusCode: 200
    handler: |
      {
        "ID": "e3b7a4a7a7a74a84b86f0e2c4b0a9b1b8d37b0e241d75b7d1f0e2cd27b3c1e55",
        "Containers": 6,
        "ContainersRunning": 6,
        "ContainersPaused": 0,
        "ContainersStopped": 0,
        "Images": 9,
        "Driver": "overlay2",
        "DriverStatus": [["Backing Filesystem","extfs"],["Supports d_type","true"],["Native Overlay Diff","true"]],
        "Plugins": {"Volume": ["local"], "Network": ["bridge","host","null"], "Log": ["json-file","local"]},
        "MemoryLimit": true,
        "SwapLimit": true,
        "KernelMemory": true,
        "CPUSet": true,
        "CPUShares": true,
        "IPv4Forwarding": true,
        "BridgeNfIptables": true,
        "BridgeNfIp6tables": true,
        "OOMKillDisable": true,
        "Warnings": null,
        "OperatingSystem": "Ubuntu 22.04.4 LTS",
        "OSVersion": "22.04",
        "OSType": "linux",
        "Architecture": "x86_64",
        "NCPU": 4,
        "MemTotal": 8178892800,
        "DockerRootDir": "/var/lib/docker",
        "HttpProxy": "",
        "HttpsProxy": "",
        "NoProxy": "",
        "Name": "li-docker-01",
        "ServerVersion": "24.0.7",
        "DefaultRuntime": "runc",
        "Runtimes": {"runc": {"path": "runc"}},
        "Swarm": {"LocalNodeState": "inactive"},
        "LiveRestoreEnabled": false
      }

  - regex: "^/images/json(?:\\?.*)?/?$"
    headers:
      - "Content-Type: application/json"
      - "Server: Docker/24.0.7 (linux)"
    statusCode: 200
    handler: |
      [
        {"Id":"sha256:0f9c7dd2b51b46a3c8b6f8a0d1e24f6f8e8dd7131f4bc779e0c5b5b2a84e83ce","RepoTags":["nginx:1.21.6"],"Size":141943872,"VirtualSize":141943872,"Created":1691577600},
        {"Id":"sha256:6ab2f8c0a2e124e5f1d6a91d5bf0cf8d3c3227e1f88e4a0e6b0f0b9f7f6f2b41","RepoTags":["redis:5.0.14"],"Size":104857600,"VirtualSize":104857600,"Created":1691664000},
        {"Id":"sha256:d1b4a12a99e5c3c2f65b2d9b49d84eb0f8a91bf2841b0a2c2b9ed5fe0c6a6a31","RepoTags":["postgres:11.12"],"Size":223346688,"VirtualSize":223346688,"Created":1691750400},
        {"Id":"sha256:3c94a0a7d7e41d9c1a03d2a46b7f54b2e3b1a6a1a7465f0abf0dd0b91a2ddee0","RepoTags":["prom/prometheus:v2.26.0"],"Size":176160768,"VirtualSize":176160768,"Created":1691836800},
        {"Id":"sha256:94c5a86f7b82b0e3e09f1ec9f8d0a7b1c5e6d237b4a9e1d9a1f0d3b2a6a7b1e9","RepoTags":["grafana/grafana:8.3.0"],"Size":278921216,"VirtualSize":278921216,"Created":1691923200},
        {"Id":"sha256:2a5ec9c0e75a4e8e9f8a17b6c5d1a7b0e93e1af2d6c6e2a9f8a3c2d4b5e6f7a8","RepoTags":["tiangolo/uvicorn-gunicorn-fastapi:python3.11"],"Size":312475648,"VirtualSize":312475648,"Created":1692009600},
        {"Id":"sha256:7a8b9c0d1e2f3a4b5c6d7e8f091a2b3c4d5e6f70a1b2c3d4e5f6a7b8c9d0e1f2","RepoTags":["alpine:3.16"],"Size":56623104,"VirtualSize":56623104,"Created":1692096000},
        {"Id":"sha256:bb51a5b13adf41a1bf67b1a2c0e5b7cd0a59ff1c99d57a1d7e64e4f5a47a2dd3","RepoTags":["busybox:1.36"],"Size":22282240,"VirtualSize":22282240,"Created":1692182400},
        {"Id":"sha256:2f8e405fd7a54d27a8f9a2e3c5d7b9e0a1c2d3e4f5a6b7c8d9e0f1a2b3c4d5e6","RepoTags":["coredns/coredns:1.11.3"],"Size":46661632,"VirtualSize":46661632,"Created":1692268800}
      ]

  - regex: "^/containers/json(?:\\?.*)?/?$"
    headers:
      - "Content-Type: application/json"
      - "Server: Docker/24.0.7 (linux)"
    statusCode: 200
    handler: |
      [
        {"Id":"a0c2c51c1f7a4b20a9cc1a0b4a9b06f3040c14b496f0f3c21bd7e0f3ae90f7b6","Names":["/web-frontend"],"Image":"nginx:1.21.6","ImageID":"sha256:0f9c7dd2b51b46a3c8b6f8a0d1e24f6f8e8dd7131f4bc779e0c5b5b2a84e83ce","Command":"nginx -g 'daemon off;'","Created":1723276934,"State":"running","Status":"Up 3 days","Ports":[{"PrivatePort":80,"Type":"tcp"}],"Labels":{"app":"web-frontend"},"HostConfig":{"NetworkMode":"bridge"},"NetworkSettings":{"Networks":{"bridge":{"IPAddress":"172.17.0.2"}}}},
        {"Id":"1df1a9b7501f4d56a4eb30b6a8e58d3ce3d0883a2df1432593a5b9eec8db4231","Names":["/api-service"],"Image":"tiangolo/uvicorn-gunicorn-fastapi:python3.11","ImageID":"sha256:2a5ec9c0e75a4e8e9f8a17b6c5d1a7b0e93e1af2d6c6e2a9f8a3c2d4b5e6f7a8","Command":"/start-reload.sh","Created":1723277131,"State":"running","Status":"Up 3 days","Ports":[{"PrivatePort":8000,"Type":"tcp"}],"Labels":{"app":"api-service"},"HostConfig":{"NetworkMode":"bridge"},"NetworkSettings":{"Networks":{"bridge":{"IPAddress":"172.17.0.3"}}}},
        {"Id":"c32e6d4f2fa54c6fb4e0a4d85f8c7f8f30bfb2b5e1c8412398e2b8a8fb2c07d1","Names":["/redis"],"Image":"redis:5.0.14","ImageID":"sha256:6ab2f8c0a2e124e5f1d6a91d5bf0cf8d3c3227e1f88e4a0e6b0f0b9f7f6f2b41","Command":"redis-server","Created":1723277160,"State":"running","Status":"Up 3 days","Ports":[{"PrivatePort":6379,"Type":"tcp"}],"Labels":{"app":"redis"},"HostConfig":{"NetworkMode":"bridge"},"NetworkSettings":{"Networks":{"bridge":{"IPAddress":"172.17.0.4"}}}},
        {"Id":"7a8e6c6c541b4e40b9a0c6f9a3c9a0024a6a1f6e24f44b63b39f2bbf31f7ea5e","Names":["/postgres"],"Image":"postgres:11.12","ImageID":"sha256:d1b4a12a99e5c3c2f65b2d9b49d84eb0f8a91bf2841b0a2c2b9ed5fe0c6a6a31","Command":"postgres","Created":1723277264,"State":"running","Status":"Up 3 days","Ports":[{"PrivatePort":5432,"Type":"tcp"}],"Labels":{"app":"postgres"},"HostConfig":{"NetworkMode":"bridge"},"NetworkSettings":{"Networks":{"bridge":{"IPAddress":"172.17.0.5"}}}},
        {"Id":"8c7b2d98c8bc4d27a74d0a9e4f4f7159d2d03b0c8e6b4a7e8c1d2a4f0c3e7b65","Names":["/prometheus"],"Image":"prom/prometheus:v2.26.0","ImageID":"sha256:3c94a0a7d7e41d9c1a03d2a46b7f54b2e3b1a6a1a7465f0abf0dd0b91a2ddee0","Command":"/bin/prometheus","Created":1723363561,"State":"running","Status":"Up 2 days","Ports":[{"PrivatePort":9090,"Type":"tcp"}],"Labels":{"app":"prometheus"},"HostConfig":{"NetworkMode":"bridge"},"NetworkSettings":{"Networks":{"bridge":{"IPAddress":"172.17.0.6"}}}},
        {"Id":"b2e9a8e2a4a841f1a1d4a2b6f8c6c1d79a6e2b7d4f1e4a6b9c2d1f5e8a3b7c2d","Names":["/grafana"],"Image":"grafana/grafana:8.3.0","ImageID":"sha256:94c5a86f7b82b0e3e09f1ec9f8d0a7b1c5e6d237b4a9e1d9a1f0d3b2a6a7b1e9","Command":"/run.sh","Created":1723364014,"State":"running","Status":"Up 2 days","Ports":[{"PrivatePort":3000,"Type":"tcp"}],"Labels":{"app":"grafana"},"HostConfig":{"NetworkMode":"bridge"},"NetworkSettings":{"Networks":{"bridge":{"IPAddress":"172.17.0.7"}}}}
      ]

  - regex: "^/images/[^/]+/json/?$"
    headers: ["Content-Type: application/json"]
    statusCode: 200
    handler: |
      {"Id":"sha256:0f9c7dd2b51b46a3c8b6f8a0d1e24f6f8e8dd7131f4bc779e0c5b5b2a84e83ce","RepoTags":["nginx:1.21.6"]}

  - regex: "^/networks/?$"
    headers: ["Content-Type: application/json"]
    statusCode: 200
    handler: |
      [
        {"Name":"bridge","Id":"f1a7b0d9a21e4ff3a9c2b4e3a51d7b4fe9e2d4a1c0b7f9034db9c5ea3c1f2a8e","Driver":"bridge","Scope":"local"},
        {"Name":"host","Id":"6d1e4b0a9f8c4c2bb0c7a9d4e1f3b2c08ca7e2b1a3f94d0ecb5a2e4c7a9b0d3f","Driver":"host","Scope":"local"},
        {"Name":"none","Id":"2ce7a9d10b3f4a6c8e9d0a1b2c3d4e5f60718293a4b5c6d7e8f9012a3b4c5d6e","Driver":"null","Scope":"local"}
      ]

  - regex: "^/volumes/?$"
    headers: ["Content-Type: application/json"]
    statusCode: 200
    handler: |
      {"Volumes":[
        {"CreatedAt":"2025-08-10T08:00:21Z","Driver":"local","Labels":null,"Mountpoint":"/var/lib/docker/volumes/pgdata/_data","Name":"pgdata","Scope":"local"},
        {"CreatedAt":"2025-08-11T09:15:09Z","Driver":"local","Labels":null,"Mountpoint":"/var/lib/docker/volumes/prom-data/_data","Name":"prom-data","Scope":"local"}
      ],"Warnings":null}

  - regex: "^/system/df/?$"
    headers: ["Content-Type: application/json"]
    statusCode: 200
    handler: |
      {"LayersSize":652738560,"Images":[{"Id":"sha256:0f9c7dd2b51b46a3c8b6f8a0d1e24f6f8e8dd7131f4bc779e0c5b5b2a84e83ce","Size":141943872},{"Id":"sha256:d1b4a12a99e5c3c2f65b2d9b49d84eb0f8a91bf2841b0a2c2b9ed5fe0c6a6a31","Size":223346688}],"Containers":[{"Id":"a0c2c51c1f7a4b20a9cc1a0b4a9b06f3040c14b496f0f3c21bd7e0f3ae90f7b6","SizeRootFs":73400320}]}

  - regex: "^/events(?:\\?.*)?/?$"
    headers: ["Content-Type: application/json"]
    statusCode: 200
    handler: |
      {"status":"start","id":"a0c2c51c1f7a4b20a9cc1a0b4a9b06f3040c14b496f0f3c21bd7e0f3ae90f7b6","from":"nginx:1.21.6","Type":"container","time":1723815011}
      {"status":"health_status: healthy","id":"1df1a9b7501f4d56a4eb30b6a8e58d3ce3d0883a2df1432593a5b9eec8db4231","from":"tiangolo/uvicorn-gunicorn-fastapi:python3.11","Type":"container","time":1723815059}

  - regex: "^/(v1\\.(4[0-9]|3[0-9]))?/images/json$"
    headers:
      - "Content-Type: application/json"
      - "Server: Docker/24.0.7 (linux)"
    statusCode: 200
    handler: |
      [
        {"Id":"sha256:0f9c7dd2b51b46a3c8b6f8a0d1e24f6f8e8dd7131f4bc779e0c5b5b2a84e83ce","RepoTags":["nginx:1.21.6"],"Size":141943872,"VirtualSize":141943872,"Created":1691577600},
        {"Id":"sha256:6ab2f8c0a2e124e5f1d6a91d5bf0cf8d3c3227e1f88e4a0e6b0f0b9f7f6f2b41","RepoTags":["redis:5.0.14"],"Size":104857600,"VirtualSize":104857600,"Created":1691664000},
        {"Id":"sha256:d1b4a12a99e5c3c2f65b2d9b49d84eb0f8a91bf2841b0a2c2b9ed5fe0c6a6a31","RepoTags":["postgres:11.12"],"Size":223346688,"VirtualSize":223346688,"Created":1691750400},
        {"Id":"sha256:3c94a0a7d7e41d9c1a03d2a46b7f54b2e3b1a6a1a7465f0abf0dd0b91a2ddee0","RepoTags":["prom/prometheus:v2.26.0"],"Size":176160768,"VirtualSize":176160768,"Created":1691836800},
        {"Id":"sha256:94c5a86f7b82b0e3e09f1ec9f8d0a7b1c5e6d237b4a9e1d9a1f0d3b2a6a7b1e9","RepoTags":["grafana/grafana:8.3.0"],"Size":278921216,"VirtualSize":278921216,"Created":1691923200},
        {"Id":"sha256:2a5ec9c0e75a4e8e9f8a17b6c5d1a7b0e93e1af2d6c6e2a9f8a3c2d4b5e6f7a8","RepoTags":["tiangolo/uvicorn-gunicorn-fastapi:python3.11"],"Size":312475648,"VirtualSize":312475648,"Created":1692009600},
        {"Id":"sha256:7a8b9c0d1e2f3a4b5c6d7e8f091a2b3c4d5e6f70a1b2c3d4e5f6a7b8c9d0e1f2","RepoTags":["alpine:3.16"],"Size":56623104,"VirtualSize":56623104,"Created":1692096000},
        {"Id":"sha256:bb51a5b13adf41a1bf67b1a2c0e5b7cd0a59ff1c99d57a1d7e64e4f5a47a2dd3","RepoTags":["busybox:1.36"],"Size":22282240,"VirtualSize":22282240,"Created":1692182400},
        {"Id":"sha256:2f8e405fd7a54d27a8f9a2e3c5d7b9e0a1c2d3e4f5a6b7c8d9e0f1a2b3c4d5e6","RepoTags":["coredns/coredns:1.11.3"],"Size":46661632,"VirtualSize":46661632,"Created":1692268800}
      ]

  - regex: "^/(v1\\.(4[0-9]|3[0-9]))?/containers/json.*$"
    headers:
      - "Content-Type: application/json"
      - "Server: Docker/24.0.7 (linux)"
    statusCode: 200
    handler: |
      [
        {"Id":"a0c2c51c1f7a4b20a9cc1a0b4a9b06f3040c14b496f0f3c21bd7e0f3ae90f7b6","Names":["/web-frontend"],"Image":"nginx:1.21.6","ImageID":"sha256:0f9c7dd2b51b46a3c8b6f8a0d1e24f6f8e8dd7131f4bc779e0c5b5b2a84e83ce","Command":"nginx -g 'daemon off;'","Created":1723276934,"State":"running","Status":"Up 3 days","Ports":[{"PrivatePort":80,"Type":"tcp"}],"Labels":{"app":"web-frontend"},"HostConfig":{"NetworkMode":"bridge"},"NetworkSettings":{"Networks":{"bridge":{"IPAddress":"172.17.0.2"}}}},
        {"Id":"1df1a9b7501f4d56a4eb30b6a8e58d3ce3d0883a2df1432593a5b9eec8db4231","Names":["/api-service"],"Image":"tiangolo/uvicorn-gunicorn-fastapi:python3.11","ImageID":"sha256:2a5ec9c0e75a4e8e9f8a17b6c5d1a7b0e93e1af2d6c6e2a9f8a3c2d4b5e6f7a8","Command":"/start-reload.sh","Created":1723277131,"State":"running","Status":"Up 3 days","Ports":[{"PrivatePort":8000,"Type":"tcp"}],"Labels":{"app":"api-service"},"HostConfig":{"NetworkMode":"bridge"},"NetworkSettings":{"Networks":{"bridge":{"IPAddress":"172.17.0.3"}}}},
        {"Id":"c32e6d4f2fa54c6fb4e0a4d85f8c7f8f30bfb2b5e1c8412398e2b8a8fb2c07d1","Names":["/redis"],"Image":"redis:5.0.14","ImageID":"sha256:6ab2f8c0a2e124e5f1d6a91d5bf0cf8d3c3227e1f88e4a0e6b0f0b9f7f6f2b41","Command":"redis-server","Created":1723277160,"State":"running","Status":"Up 3 days","Ports":[{"PrivatePort":6379,"Type":"tcp"}],"Labels":{"app":"redis"},"HostConfig":{"NetworkMode":"bridge"},"NetworkSettings":{"Networks":{"bridge":{"IPAddress":"172.17.0.4"}}}}
      ]

  - regex: "^/(v1\\.(4[0-9]|3[0-9]))?/containers/a0c2c51c1f7a4b20a9cc1a0b4a9b06f3040c14b496f0f3c21bd7e0f3ae90f7b6/json$"
    headers: ["Content-Type: application/json"]
    statusCode: 200
    handler: |
      {"Id":"a0c2c51c1f7a4b20a9cc1a0b4a9b06f3040c14b496f0f3c21bd7e0f3ae90f7b6","Name":"/web-frontend","Path":"nginx","Args":["-g","daemon off;"],"Image":"nginx:1.21.6","ImageID":"sha256:0f9c7dd2b51b46a3c8b6f8a0d1e24f6f8e8dd7131f4bc779e0c5b5b2a84e83ce","Created":"2025-08-10T08:02:14Z","State":{"Status":"running","Running":true,"StartedAt":"2025-08-10T08:02:25Z","Pid":2157},"Config":{"Hostname":"a0c2c51c1f7a","Env":["NGINX_VERSION=1.21.6"],"ExposedPorts":{"80/tcp":{}}},"HostConfig":{"NetworkMode":"bridge"},"NetworkSettings":{"Networks":{"bridge":{"IPAddress":"172.17.0.2"}}}}

  - regex: "^/(v1\\.(4[0-9]|3[0-9]))?/containers/1df1a9b7501f4d56a4eb30b6a8e58d3ce3d0883a2df1432593a5b9eec8db4231/json$"
    headers: ["Content-Type: application/json"]
    statusCode: 200
    handler: |
      {"Id":"1df1a9b7501f4d56a4eb30b6a8e58d3ce3d0883a2df1432593a5b9eec8db4231","Name":"/api-service","Image":"tiangolo/uvicorn-gunicorn-fastapi:python3.11","ImageID":"sha256:2a5ec9c0e75a4e8e9f8a17b6c5d1a7b0e93e1af2d6c6e2a9f8a3c2d4b5e6f7a8","Created":"2025-08-10T08:05:31Z","State":{"Status":"running","Running":true,"StartedAt":"2025-08-10T08:05:45Z","Pid":2298},"Path":"/start-reload.sh","Args":[],"Config":{"Env":["PORT=8000"],"ExposedPorts":{"8000/tcp":{}}},"HostConfig":{"NetworkMode":"bridge"},"NetworkSettings":{"Networks":{"bridge":{"IPAddress":"172.17.0.3"}}}}

  - regex: "^/(v1\\.(4[0-9]|3[0-9]))?/containers/c32e6d4f2fa54c6fb4e0a4d85f8c7f8f30bfb2b5e1c8412398e2b8a8fb2c07d1/json$"
    headers: ["Content-Type: application/json"]
    statusCode: 200
    handler: |
      {"Id":"c32e6d4f2fa54c6fb4e0a4d85f8c7f8f30bfb2b5e1c8412398e2b8a8fb2c07d1","Name":"/redis","Image":"redis:5.0.14","ImageID":"sha256:6ab2f8c0a2e124e5f1d6a91d5bf0cf8d3c3227e1f88e4a0e6b0f0b9f7f6f2b41","Created":"2025-08-10T08:06:00Z","State":{"Status":"running","Running":true,"StartedAt":"2025-08-10T08:06:12Z","Pid":2332},"Path":"redis-server","Args":[],"Config":{"Env":["REDIS_VERSION=5.0.14"],"ExposedPorts":{"6379/tcp":{}}},"HostConfig":{"NetworkMode":"bridge"},"NetworkSettings":{"Networks":{"bridge":{"IPAddress":"172.17.0.4"}}}}

  - regex: "^/(v1\\.(4[0-9]|3[0-9]))?/containers/7a8e6c6c541b4e40b9a0c6f9a3c9a0024a6a1f6e24f44b63b39f2bbf31f7ea5e/json$"
    headers: ["Content-Type: application/json"]
    statusCode: 200
    handler: |
      {"Id":"7a8e6c6c541b4e40b9a0c6f9a3c9a0024a6a1f6e24f44b63b39f2bbf31f7ea5e","Name":"/postgres","Image":"postgres:11.12","ImageID":"sha256:d1b4a12a99e5c3c2f65b2d9b49d84eb0f8a91bf2841b0a2c2b9ed5fe0c6a6a31","Created":"2025-08-10T08:07:44Z","State":{"Status":"running","Running":true,"StartedAt":"2025-08-10T08:07:59Z","Pid":2409},"Path":"postgres","Args":[],"Config":{"Env":["POSTGRES_VERSION=11.12"],"ExposedPorts":{"5432/tcp":{}}},"HostConfig":{"NetworkMode":"bridge"},"NetworkSettings":{"Networks":{"bridge":{"IPAddress":"172.17.0.5"}}}}

  - regex: "^/(v1\\.(4[0-9]|3[0-9]))?/containers/8c7b2d98c8bc4d27a74d0a9e4f4f7159d2d03b0c8e6b4a7e8c1d2a4f0c3e7b65/json$"
    headers: ["Content-Type: application/json"]
    statusCode: 200
    handler: |
      {"Id":"8c7b2d98c8bc4d27a74d0a9e4f4f7159d2d03b0c8e6b4a7e8c1d2a4f0c3e7b65","Name":"/prometheus","Image":"prom/prometheus:v2.26.0","ImageID":"sha256:3c94a0a7d7e41d9c1a03d2a46b7f54b2e3b1a6a1a7465f0abf0dd0b91a2ddee0","Created":"2025-08-11T09:12:41Z","State":{"Status":"running","Running":true,"StartedAt":"2025-08-11T09:12:58Z","Pid":3127},"Path":"/bin/prometheus","Args":[],"Config":{"ExposedPorts":{"9090/tcp":{}}},"HostConfig":{"NetworkMode":"bridge"},"NetworkSettings":{"Networks":{"bridge":{"IPAddress":"172.17.0.6"}}}}

  - regex: "^/(v1\\.(4[0-9]|3[0-9]))?/containers/b2e9a8e2a4a841f1a1d4a2b6f8c6c1d79a6e2b7d4f1e4a6b9c2d1f5e8a3b7c2d/json$"
    headers: ["Content-Type: application/json"]
    statusCode: 200
    handler: |
      {"Id":"b2e9a8e2a4a841f1a1d4a2b6f8c6c1d79a6e2b7d4f1e4a6b9c2d1f5e8a3b7c2d","Name":"/grafana","Image":"grafana/grafana:8.3.0","ImageID":"sha256:94c5a86f7b82b0e3e09f1ec9f8d0a7b1c5e6d237b4a9e1d9a1f0d3b2a6a7b1e9","Created":"2025-08-11T09:20:14Z","State":{"Status":"running","Running":true,"StartedAt":"2025-08-11T09:20:28Z","Pid":3196},"Path":"/run.sh","Args":[],"Config":{"ExposedPorts":{"3000/tcp":{}}},"HostConfig":{"NetworkMode":"bridge"},"NetworkSettings":{"Networks":{"bridge":{"IPAddress":"172.17.0.7"}}}}

  - regex: "^/(v1\\.(4[0-9]|3[0-9]))?/containers/a0c2c51c1f7a4b20a9cc1a0b4a9b06f3040c14b496f0f3c21bd7e0f3ae90f7b6/logs.*$"
    headers: ["Content-Type: text/plain; charset=utf-8"]
    statusCode: 200
    handler: |
      2025-08-15T08:10:07Z 172.17.0.1 - - "GET / HTTP/1.1" 200 612 "-" "curl/8.4.0"

  - regex: "^/(v1\\.(4[0-9]|3[0-9]))?/containers/1df1a9b7501f4d56a4eb30b6a8e58d3ce3d0883a2df1432593a5b9eec8db4231/logs.*$"
    headers: ["Content-Type: text/plain; charset=utf-8"]
    statusCode: 200
    handler: |
      INFO uvicorn.access: 172.17.0.1 - "GET /health HTTP/1.1" 200

  - regex: "^/(v1\\.(4[0-9]|3[0-9]))?/containers/c32e6d4f2fa54c6fb4e0a4d85f8c7f8f30bfb2b5e1c8412398e2b8a8fb2c07d1/logs.*$"
    headers: ["Content-Type: text/plain; charset=utf-8"]
    statusCode: 200
    handler: |
      * Ready to accept connections (Redis 5.0.14) on 0.0.0.0:6379

  - regex: "^/(v1\\.(4[0-9]|3[0-9]))?/containers/7a8e6c6c541b4e40b9a0c6f9a3c9a0024a6a1f6e24f44b63b39f2bbf31f7ea5e/logs.*$"
    headers: ["Content-Type: text/plain; charset=utf-8"]
    statusCode: 200
    handler: |
      database system is ready to accept connections (PostgreSQL 11.12)

  - regex: "^/(v1\\.(4[0-9]|3[0-9]))?/containers/8c7b2d98c8bc4d27a74d0a9e4f4f7159d2d03b0c8e6b4a7e8c1d2a4f0c3e7b65/logs.*$"
    headers: ["Content-Type: text/plain; charset=utf-8"]
    statusCode: 200
    handler: |
      level=info ts=2025-08-15T08:10:11Z caller=head.go:916 msg="WAL segment loaded" bytes=16777216

  - regex: "^/(v1\\.(4[0-9]|3[0-9]))?/containers/b2e9a8e2a4a841f1a1d4a2b6f8c6c1d79a6e2b7d4f1e4a6b9c2d1f5e8a3b7c2d/logs.*$"
    headers: ["Content-Type: text/plain; charset=utf-8"]
    statusCode: 200
    handler: |
      logger=server t=2025-08-15T08:10:11Z level=info msg="HTTP Server Listen" address=0.0.0.0:3000 protocol=http

  - regex: "^/(v1\\.(4[0-9]|3[0-9]))?/containers/[^/]+/top.*$"
    headers: ["Content-Type: application/json"]
    statusCode: 200
    handler: |
      {"Titles":["PID","USER","TIME","COMMAND"],"Processes":[["2157","root","00:00:12","nginx: master process nginx -g daemon off;"]]}

  - regex: "^/(v1\\.(4[0-9]|3[0-9]))?/containers/[^/]+/stats.*$"
    headers: ["Content-Type: application/json"]
    statusCode: 200
    handler: |
      {"read":"2025-08-15T08:10:11Z","pids_stats":{"current":6},"cpu_stats":{"cpu_usage":{"total_usage":123456789}},"memory_stats":{"usage":73400320,"limit":8178892800},"networks":{"eth0":{"rx_bytes":10240,"tx_bytes":20480}}}

  # ---------- Exec (create/json/start) ----------
  - regex: "^/(v1\\.(4[0-9]|3[0-9]))?/containers/[^/]+/exec$"
    headers: ["Content-Type: application/json"]
    statusCode: 201
    handler: |
      {"Id":"e8b3f7b41e0b4b1fa41e3c6d7c0f9a24d93ab2e2f41d4ce78b6c93f0a1b7404f"}

  - regex: "^/(v1\\.(4[0-9]|3[0-9]))?/exec/[^/]+/json$"
    headers: ["Content-Type: application/json"]
    statusCode: 200
    handler: |
      {"ID":"e8b3f7b41e0b4b1fa41e3c6d7c0f9a24d93ab2e2f41d4ce78b6c93f0a1b7404f","Running":false,"ExitCode":0,"OpenStdin":false,"OpenStderr":true,"OpenStdout":true}

  - regex: "^/(v1\\.(4[0-9]|3[0-9]))?/exec/[^/]+/start$"
    headers: ["Content-Type: application/json"]
    statusCode: 200
    handler: |
      {"ok":true}

  - regex: "^/(v1\\.(4[0-9]|3[0-9]))?/containers/create.*$"
    headers: ["Content-Type: application/json"]
    statusCode: 201
    handler: |
      {"Id":"6c8c4fba3f1d40d789b51f1a34d92f0cb3e19b7ef1a44d38a2a0f0f51c4a0c8d","Warnings":null}

  - regex: "^/(v1\\.(4[0-9]|3[0-9]))?/containers/[^/]+/(start|stop|restart|kill)$"
    headers: ["Content-Type: application/json"]
    statusCode: 204
    handler: ""

  - regex: "^/(v1\\.(4[0-9]|3[0-9]))?/containers/[^/]+$"
    headers: ["Content-Type: application/json"]
    statusCode: 204
    handler: ""

  - regex: "^/(v1\\.(4[0-9]|3[0-9]))?/images/[^/]+/json$"
    headers: ["Content-Type: application/json"]
    statusCode: 200
    handler: |
      {"Id":"sha256:0f9c7dd2b51b46a3c8b6f8a0d1e24f6f8e8dd7131f4bc779e0c5b5b2a84e83ce","RepoTags":["nginx:1.21.6"]}

  - regex: "^/(v1\\.(4[0-9]|3[0-9]))?/networks$"
    headers: ["Content-Type: application/json"]
    statusCode: 200
    handler: |
      [
        {"Name":"bridge","Id":"f1a7b0d9a21e4ff3a9c2b4e3a51d7b4fe9e2d4a1c0b7f9034db9c5ea3c1f2a8e","Driver":"bridge","Scope":"local"},
        {"Name":"host","Id":"6d1e4b0a9f8c4c2bb0c7a9d4e1f3b2c08ca7e2b1a3f94d0ecb5a2e4c7a9b0d3f","Driver":"host","Scope":"local"},
        {"Name":"none","Id":"2ce7a9d10b3f4a6c8e9d0a1b2c3d4e5f60718293a4b5c6d7e8f9012a3b4c5d6e","Driver":"null","Scope":"local"}
      ]

  - regex: "^/(v1\\.(4[0-9]|3[0-9]))?/volumes$"
    headers: ["Content-Type: application/json"]
    statusCode: 200
    handler: |
      {"Volumes":[
        {"CreatedAt":"2025-08-10T08:00:21Z","Driver":"local","Labels":null,"Mountpoint":"/var/lib/docker/volumes/pgdata/_data","Name":"pgdata","Scope":"local"},
        {"CreatedAt":"2025-08-11T09:15:09Z","Driver":"local","Labels":null,"Mountpoint":"/var/lib/docker/volumes/prom-data/_data","Name":"prom-data","Scope":"local"}
      ],"Warnings":null}

  - regex: "^/(v1\\.(4[0-9]|3[0-9]))?/system/df$"
    headers: ["Content-Type: application/json"]
    statusCode: 200
    handler: |
      {"LayersSize":652738560,"Images":[{"Id":"sha256:0f9c7dd2b51b46a3c8b6f8a0d1e24f6f8e8dd7131f4bc779e0c5b5b2a84e83ce","Size":141943872},{"Id":"sha256:d1b4a12a99e5c3c2f65b2d9b49d84eb0f8a91bf2841b0a2c2b9ed5fe0c6a6a31","Size":223346688}],"Containers":[{"Id":"a0c2c51c1f7a4b20a9cc1a0b4a9b06f3040c14b496f0f3c21bd7e0f3ae90f7b6","SizeRootFs":73400320}]}

  - regex: "^/(v1\\.(4[0-9]|3[0-9]))?/(containers|images)/(prune)$"
    headers: ["Content-Type: application/json"]
    statusCode: 200
    handler: |
      {"SpaceReclaimed":0}

  - regex: "^/(v1\\.(4[0-9]|3[0-9]))?/swarm/leave$"
    headers:
      - "Content-Type: application/json"
    statusCode: 200
    handler: |
      {"message":"Node left the swarm."}

  - regex: "^/v1\\..*$"
    headers: ["Content-Type: text/plain; charset=utf-8"]
    statusCode: 404
    handler: "page not found"

  - regex: "^/$"
    headers: ["Content-Type: text/plain; charset=utf-8"]
    statusCode: 404
    handler: "page not found"

  - regex: "^.*$"
    headers: ["Content-Type: text/plain; charset=utf-8"]
    statusCode: 404
    handler: "page not found"
```
