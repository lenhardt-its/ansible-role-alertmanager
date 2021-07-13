# Ansible Role: Alertmanager

[![ubuntu-18](https://img.shields.io/badge/ubuntu-18.x-orange?style=flat&logo=ubuntu)](https://ubuntu.com/)
[![ubuntu-20](https://img.shields.io/badge/ubuntu-20.x-orange?style=flat&logo=ubuntu)](https://ubuntu.com/)
[![debian-9](https://img.shields.io/badge/debian-9.x-orange?style=flat&logo=debian)](https://www.debian.org/)
[![debian-10](https://img.shields.io/badge/debian-10.x-orange?style=flat&logo=debian)](https://www.debian.org/)
[![centos-7](https://img.shields.io/badge/centos-7.x-orange?style=flat&logo=centos)](https://www.centos.org/)
[![centos-8](https://img.shields.io/badge/centos-8.x-orange?style=flat&logo=centos)](https://www.centos.org/)

[![License](https://img.shields.io/badge/license-MIT%20License-brightgreen.svg?style=flat)](https://opensource.org/licenses/MIT)
[![GitHub issues](https://img.shields.io/github/issues/OnkelDom/ansible-role-alertmanager?style=flat)](https://github.com/OnkelDom/ansible-role-alertmanager/issues)
[![GitHub tag](https://img.shields.io/github/tag/OnkelDom/ansible-role-alertmanager.svg?style=flat)](https://github.com/OnkelDom/ansible-role-alertmanager/tags)
[![GitHub action](https://github.com/OnkelDom/ansible-role-alertmanager/workflows/ansible-lint/badge.svg)](https://github.com/OnkelDom/ansible-role-alertmanager)

## Description

Deploy and manage Prometheus [alertmanager](https://github.com/prometheus/alertmanager) service using ansible.

## Requirements

- Ansible >= 2.9 (It might work on previous versions, but we cannot guarantee it)

## Role Variables

All variables which can be overridden are stored in [defaults/main.yml](defaults/main.yml) file as well as in table below.

| Name           | Default Value | Description                        |
| -------------- | ------------- | -----------------------------------|
| `proxy_env` | {} | Proxy environment variables for Client|
| `alertmanager_version` | 0.21.0 | Alertmanager package version. Also accepts `latest` as parameter. |
| `alertmanager_web_listen_address` | 0.0.0.0:9093 | Address on which alertmanager will be listening |
| `alertmanager_web_external_url` | http://localhost:9093/ | External address on which alertmanager is available. Useful when behind reverse proxy. Ex. example.org/alertmanager |
| `alertmanager_config_dir` | /etc/alertmanager | Path to directory with alertmanager configuration |
| `alertmanager_db_dir` | /var/lib/alertmanager | Path to directory with alertmanager database |
| `alertmanager_config_file` | alertmanager.yml.j2 | Variable used to provide custom alertmanager configuration file in form of ansible template |
| `alertmanager_config_flags_extra` | {} | Additional configuration flags passed to prometheus binary at startup |
| `alertmanager_template_files` | ['alertmanager/templates/*.tmpl'] | List of folders where ansible will look for template files which will be copied to `{{ alertmanager_config_dir }}/templates/`. Files must have `*.tmpl` extension |
| `alertmanager_resolve_timeout` | 3m | Time after which an alert is declared resolved |
| `alertmanager_smtp` | {} | SMTP (email) configuration |
| `alertmanager_slack_api_url` | "" | Slack webhook url |
| `alertmanager_pagerduty_url` | "" | Pagerduty webhook url |
| `alertmanager_opsgenie_api_key` | "" | Opsgenie webhook key |
| `alertmanager_opsgenie_api_url` | "" | Opsgenie webhook url |
| `alertmanager_hipchat_api_url` | "" | Hipchat webhook url |
| `alertmanager_hipchat_auth_token` | "" | Hipchat authentication token |
| `alertmanager_wechat_url` | "" | Enterprise WeChat webhook url |
| `alertmanager_wechat_secret` | "" | Enterprise WeChat secret token |
| `alertmanager_wechat_corp_id` | "" | Enterprise WeChat corporation id |
| `alertmanager_cluster` | {listen-address: ""} | HA cluster network configuration. Disabled by default. More information in [alertmanager readme](https://github.com/prometheus/alertmanager#high-availability) |
| `alertmanager_receivers` | [] | A list of notification receivers. Configuration same as in [official docs](https://prometheus.io/docs/alerting/configuration/#<receiver>) |
| `alertmanager_inhibit_rules` | [] | List of inhibition rules. Same as in [official docs](https://prometheus.io/docs/alerting/configuration/#inhibit_rule) |
| `alertmanager_route` | {} | Alert routing. More in [official docs](https://prometheus.io/docs/alerting/configuration/#<route>) |
| `alertmanager_child_routes` | [] | List of child routes. |
| -------------- | ------------- | -----------------------------------|
| `alertmanager_binary_local_dir` | /usr/local/bin | |
| `alertmanager_config_dir` | /etc/alertmanager | |
| `alertmanager_db_dir` | /var/lib/alertmanager | |
| `alertmanager_system_user` | prometheus | |
| `alertmanager_system_group` | prometheus | |
| `alertmanager_log_level ` | warn | |
| `alertmanager_log_format` | json | |
| `alertmanager_web_listen_port:` | 9093 | |
| `alertmanager_web_listen_address` | "0.0.0.0" | |
| `alertmanager_create_consul_agent_service` | true | |
| `alertmanager_web_external_url` | "http://{{ ansible_domain }}.{{ ansible_hostname }}:{{ alertmanager_web_listen_port }}/" | |

## Example

### Playbook

```yaml
- hosts: all
  roles:
    - onkeldom.alertmanager
```

## Contributing

See [contributor guideline](CONTRIBUTING.md).

## License

This project is licensed under MIT License. See [LICENSE](/LICENSE) for more details.
