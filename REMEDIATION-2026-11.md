# Script remediation — 8 November 2026

node_exporter installation now depends on actual desired-version state, not whether a checksum file happened to change. Archive download uses get_url checksum verification before local extraction; unsupported checksum on unarchive is removed. Private temporary staging is removed in always; retries after interrupted downloads remain eligible. Only reviewed amd64 platform/version input accepted. Binary replacement notifies the existing restart handler.

Nothing deployed. Local YAML/source checks do not validate package/firewall/service behavior. Required lab: checksum mismatch, interrupted download/copy, same-version rerun, upgrade/restart, RHEL package/firewall inventory. Trust upstream release checksums and pin approved versions; do not invent a digest. Existing broad baseline configuration, Kubernetes policy and dependency pinning require environment review. No benchmark claims.

Local validation and PR CI use syntax/static checks only, plus mocked storage preflight where applicable; infrastructure integration remains unverified.

## Variable migration (breaking)

Role variables and registered results now use role prefixes; update external inventory/Vault overrides before applying. All in-repository references were migrated.

| Previous variable | Replacement |
|---|---|
| `baseline_admin_users` | `common_baseline_baseline_admin_users` |
| `baseline_disable_root_ssh_login` | `common_baseline_baseline_disable_root_ssh_login` |
| `baseline_disable_ssh_password_auth` | `common_baseline_baseline_disable_ssh_password_auth` |
| `baseline_enable_dnf_automatic` | `common_baseline_baseline_enable_dnf_automatic` |
| `baseline_firewall_extra_services` | `common_baseline_baseline_firewall_extra_services` |
| `baseline_ntp_servers` | `common_baseline_baseline_ntp_servers` |
| `baseline_sudo_nopasswd` | `common_baseline_baseline_sudo_nopasswd` |
| `baseline_timezone` | `common_baseline_baseline_timezone` |
| `compose_result` | `monitoring_server_compose_result` |
| `grafana_admin_password` | `monitoring_server_grafana_admin_password` |
| `grafana_admin_user` | `monitoring_server_grafana_admin_user` |
| `monitoring_allowed_source_cidr` | `monitoring_server_monitoring_allowed_source_cidr` |
| `monitoring_install_dir` | `monitoring_server_monitoring_install_dir` |
| `selinux_result` | `common_baseline_selinux_result` |

Validation update: local yamllint, Ansible syntax check and ansible-lint basic profile pass after migrating role-variable names. CI no longer suppresses lint failures. No infrastructure play was executed.

Grafana preflight rejects unchanged placeholder secrets. Supply a protected Vault value using the migrated variable name; no production secret was supplied or tested.
