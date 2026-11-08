# Script remediation — 8 November 2026

node_exporter installation now depends on actual desired-version state, not whether a checksum file happened to change. Archive download uses get_url checksum verification before local extraction; unsupported checksum on unarchive is removed. Private temporary staging is removed in always; retries after interrupted downloads remain eligible. Only reviewed amd64 platform/version input accepted. Binary replacement notifies the existing restart handler.

Nothing deployed. Local YAML/source checks do not validate package/firewall/service behavior. Required lab: checksum mismatch, interrupted download/copy, same-version rerun, upgrade/restart, RHEL package/firewall inventory. Trust upstream release checksums and pin approved versions; do not invent a digest. Existing broad baseline configuration, Kubernetes policy and dependency pinning require environment review. No benchmark claims.

Local validation: YAML parsing; VMware PowerCLI connection-scope/failure/WWPN/JSON fixtures passed in PowerShell 7.4.13 for the migration repository. Windows versions and Ansible contracts are checked by the PR CI; infrastructure integration remains unverified.
