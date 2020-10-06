# Ansible Role: alertmanager

## Description

Deploy and manage Prometheus [alertmanager](https://github.com/prometheus/alertmanager) service using ansible.

## Requirements

- Ansible >= 2.6 (It might work on previous versions, but we cannot guarantee it)

## Role Variables

All variables which can be overridden are stored in [defaults/main.yml](defaults/main.yml) file as well as in table below.

| Name           | Default Value | Description                        |
| -------------- | ------------- | -----------------------------------|
| `proxy_env` | {} | Proxy environment variables |
| `alertmanager_create_consul_agent_service` | "true" | Add consul agent config snipped |
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
| `alertmanager_firewalld_state` | "disabled" | |
| `alertmanager_config_dir` | /etc/alertmanager | |
| `alertmanager_db_dir` | /var/lib/alertmanager | |
| `alertmanager_system_user` | "{{ prometheus_user | default('prometheus') }}" | |
| `alertmanager_system_group` | "{{ prometheus_group | default('prometheus') }}" | |
| `alertmanager_log_level ` | warn | |
| `alertmanager_log_format` | json | |
| `alertmanager_web_listen_port:` | 909 | |
| `alertmanager_web_listen_address` | "0.0.0.0" | |
| `alertmanager_create_consul_agent_service` | true | |
| `alertmanager_web_external_url` | "http://localhost:9093/" | |

## Example

### Playbook

```yaml
- hosts: all
  roles:
    - ansible-role-alertmanager
```

## Contributing

See [contributor guideline](CONTRIBUTING.md).

## License

This project is licensed under MIT License. See [LICENSE](/LICENSE) for more details.
