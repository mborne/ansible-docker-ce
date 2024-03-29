# docker-bench-security - uncovered items by the playbook or default values

Review of the results of [docker-bench-for-security](https://github.com/docker/docker-bench-security#docker-bench-for-security) with default config :

```bash
docker run --rm --net host --pid host --userns host --cap-add audit_control \
    -e DOCKER_CONTENT_TRUST=$DOCKER_CONTENT_TRUST \
    -v /etc:/etc:ro \
    -v /usr/bin/containerd:/usr/bin/containerd:ro \
    -v /usr/bin/runc:/usr/bin/runc:ro \
    -v /usr/lib/systemd:/usr/lib/systemd:ro \
    -v /var/lib:/var/lib:ro \
    -v /var/run/docker.sock:/var/run/docker.sock:ro \
    --label docker_bench_security \
    docker/docker-bench-security
```

## 1 - Host Configuration

* Note that you may fix this changing `data-root` that is defaulted to `/var/lib/docker` :

> [WARN] 1.1  - Ensure a separate partition for containers has been created

* Note that `auditd` is not configured by this playbook :

> [WARN] 1.5  - Ensure auditing is configured for the Docker daemon
> [WARN] 1.6  - Ensure auditing is configured for Docker files and directories - /var/lib/docker
> [WARN] 1.7  - Ensure auditing is configured for Docker files and directories - /etc/docker
> [WARN] 1.8  - Ensure auditing is configured for Docker files and directories - docker.service
> [WARN] 1.9  - Ensure auditing is configured for Docker files and directories - docker.socket
> [WARN] 1.10  - Ensure auditing is configured for Docker files and directories - /etc/default/docker
> [WARN] 1.11  - Ensure auditing is configured for Docker files and directories - /etc/docker/daemon.json

## 2 - Docker daemon configuration

* Note that you may fix this using `docker_userns_remap: 'default'` :

```
[WARN] 2.8  - Enable user namespace support
```

* Note that [Access authorization plugin](https://docs.docker.com/engine/extend/plugins_authorization/) is not covered by this playbook

```
[WARN] 2.11  - Ensure that authorization for Docker client commands is enabled
```

* Note that this playbooks doesn't supports `log-opts` option [to configure logging drivers](https://docs.docker.com/config/containers/logging/configure/) :

```
[WARN] 2.12  - Ensure centralized and remote logging is configured
```

## 3 - Docker daemon configuration files

Nothing to report.

## 4 - Container Images and Build File

Nothing to report (runtime specific)

## 5 - Container Runtime

Nothing to report (runtime specific)

## 6 - Docker Security Operations

Nothing to report (runtime specific)

## 7 - Docker Swarm Configuration

Nothing to report (swarm is not enabled)

