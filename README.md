# Ansible Role: teamcity

[![CI](https://github.com/dcjulian29/ansible-role-teamcity/actions/workflows/ci.yml/badge.svg)](https://github.com/dcjulian29/ansible-role-teamcity/actions/workflows/ci.yml) [![GitHub Issues](https://img.shields.io/github/issues-raw/dcjulian29/ansible-role-teamcity.svg)](https://github.com/dcjulian29/ansible-role-teamcity/issues)

This an Ansible role to install a Teamcity Linux based agent with docker support or a Teamcity Server. Both run within a container and NGINX is also used as a reverse proxy to handle HTTPS connections.

## Requirements

- Internet Connection to download container images.

## Installation

To use, use `requirements.yml` with the following git source:

```yaml
---
roles:
- name: dcjulian29.teamcity
  src: https://github.com/dcjulian29/ansible-role-teamcity.git
  version: main
- name: dcjulian29.docker
  src: https://github.com/dcjulian29/ansible-role-docker.git
  version: main
- name: dcjulian29.nginx
  src: https://github.com/dcjulian29/ansible-role-nginx.git
  version: main
```

Then download it with `ansible-galaxy`:

```shell
ansible-galaxy install -r requirements.yml
```

## Dependencies

- None

## Role Variables

The `defaults` variables define the default values used in the play. These variables can be overridden using `group_vars` or `host_vars` or from the playbook itself.

| Variable | Default | Description |
| --: | :-- | :-- |
| teamcity_agent | `true` | Install the Teamcity agent on the target. |
| teamcity_agent_image | `jetbrains/teamcity-agent` | The name of the Teamcity agent docker image. |
| teamcity_agent_name | `teamcity_agent` | The name of the docker container running the agent image. |
| teamcity_agent_server_trusted_certificates | `[]` | Additional PEM encoded certificates files for the agent to explicitly trust. |
| teamcity_agent_token | `""` | The agent uses this token to authenticate to server, otherwise the agent will need to be manually approved. |
| teamcity_agent_version | `2022.10.1-linux-sudo` | The version tag to install. |
| teamcity_data_dir | `/opt` | The folder to store docker volumes used by the container. ||
| teamcity_database_mysql | `false` | Install MySQL JDBC driver. |
| teamcity_database_mssql | `false` | Install Microsoft SQL Server JDBC driver. |
| teamcity_database_postgre | `false` | Install Postgre SQL JDBC driver. |
| teamcity_gid | `980` | The number for the Teamcity group.|
| teamcity_group | `teamcity` | The name of the group for folder/file permissions on target.|
| teamcity_http_port | `8111` | The port that the server docker container exposes Teamcity's HTTP port. |
| teamcity_https | `false` | Should the Teamcity server be accessable via HTTPS. |
| teamcity_https_acme | `false` | Should NGIX make accomidations for ACME certificate management? |
| teamcity_name | `teamcity_server` | The name of the Teamcity server docker image.|
| teamcity_server | `true` | Install the Teamcity server on the target. |
| teamcity_server_fqdn | `<hostname>` | The fully qualified domain name. |
| teamcity_server_image | `jetbrains/teamcity-server` | The name of the Teamcity server docker image.
| teamcity_server_port | `8111` | The HTTP port to listen on. Not the same as HTTPS.
| teamcity_server_tls_cert | `/etc/ssl/certs/ssl-cert-snakeoil.pem` | A PEM encoded PKI public certificate file. |
| teamcity_server_tls_key | `/etc/ssl/private/ssl-cert-snakeoil.key` | A PEM encoded PKI private key file. |
| teamcity_server_url | `http://<hostname>:8111` | The fully qualified URI with scheme and port number. |
| teamcity_server_version | `2022.10.1` | The version tag to install.

## Example Playbook

The examples directory include one or more example playbooks.
