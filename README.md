<!--
# SPDX-License-Identifier: Apache-2.0
# SPDX-FileCopyrightText: 2025 The Linux Foundation
-->

# 🔐 Nexus Docker Login Action

Performs Docker login for all registries in a Nexus3 instance and DockerHub.
Authenticates against all Nexus3 registry ports and the DockerHub
registry in a single step.

## nexus-docker-login-action

## Usage Example

Logs in to all Nexus3 registry ports and DockerHub using the provided
credentials.

<!-- markdownlint-disable MD013 -->

```yaml
steps:
  - name: "Docker Registry Login"
    id: docker-login
    uses: lfreleng-actions/nexus-docker-login-action@main
    with:
      nexus3-registry: "nexus3.example.org"
      nexus3-user: ${{ secrets.NEXUS3_USER }}
      nexus3-password: ${{ secrets.NEXUS3_PASSWORD }}
      dockerhub-user: ${{ secrets.DOCKERHUB_USER }}
      dockerhub-password: ${{ secrets.DOCKERHUB_PASSWORD }}
```

<!-- markdownlint-enable MD013 -->

## Inputs

<!-- markdownlint-disable MD013 -->

| Name               | Required | Default | Description                              |
| ------------------ | -------- | ------- | ---------------------------------------- |
| nexus3-registry    | True     |         | Organization's Nexus registry URL        |
| nexus3-user        | True     |         | Nexus3 organization username             |
| nexus3-password    | True     |         | Nexus3 organization user's password      |
| dockerhub-user     | True     |         | DockerHub organization username          |
| dockerhub-password | True     |         | DockerHub organization user's password   |

<!-- markdownlint-enable MD013 -->

## Outputs

This action does not produce any outputs.

## Requirements/Dependencies

Docker must be available on the runner. The action uses
[docker/login-action](https://github.com/docker/login-action) to perform
authentication.

## Notes

- The action authenticates against four Nexus3 registry ports:
  - Port `10001`: Anonymous Docker access (docker/docker credentials)
  - Port `10002`: Organization credentials
  - Port `10003`: Organization credentials
  - Port `10004`: Organization credentials
- DockerHub authentication uses the `docker.io` registry.
