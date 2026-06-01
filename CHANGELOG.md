# Changelog

All notable changes to this project will be documented in this file.

## [1.1.0] - 2026-06-02

### Role - authentication_proxy

- Added support for Debian 13.
- Added support for Enterprise Linux 10.
- Added support for Ubuntu 26.04.

## [1.0.15] - 2025-06-10

### Collection

- Corrected missing or extra dependencies.

## [1.0.14] - 2025-06-10

### Collection

- Changed repository URL to use GitHub Organization.

## [1.0.13] - 2025-05-15

### Role - authentication_proxy

- Changed OS validation.

## [1.0.12] - 2025-03-10

### Role - authentication_proxy

- Fixed variable name of `duoap_rikey` to `duoap_sso_remote_identity_key`.
- Fixed include/import tasks paths.

## [1.0.11] - 2025-03-10

### Role - authentication_proxy

- Fixed Regex typo that caused failed validation.

## [1.0.10] - 2025-01-08

### Collection

- Added Changelog.
- Updated collection README documentation.

## [1.0.9] - 2024-09-06

### Role - authentication_proxy

- The `no_log` option has been added to the `duoap_service_account_password` and `duoap_sso_service_account_password` variables.  The `no_log` option has also been added to the `service_account_password` option of the `duoap_ad_clients` and `duoap_dirsync_clouds` variables.

## [1.0.8] - 2024-08-09

### Collection

- Minimum Ansible version changed from `2.14` to `2.15` due to EOL status.

## [1.0.7] - 2024-07-26

### Role - authentication_proxy

- Replaced `duoap_configure_firewalld` and `duoap_configure_ufw` variables with the `duoap_configure_firewall` and `duoap_firewall_type` variables. This allows all firewall configuration to be enabled/disabled in one variable and the default firewall type overridden in one variable.

## [1.0.6] - 2024-07-11

### Role - authentication_proxy

- Corrected the added description to the `duoap_http_ca_certs_file` variable.

## [1.0.5] - 2024-07-11

### Role - authentication_proxy

- Added some extra description for the `duoap_http_ca_certs_file` variable.

## [1.0.4] - 2024-07-11

### Role - authentication_proxy

- Changed `duoap_configure_dirsync` variable to `duoap_dirsync_clouds` variable to allow for multiple directories to be synchronized.
- Added validation for role variables where possible.

## [1.0.3] - 2024-07-08

### Role - authentication_proxy

- Added step to gather facts regarding the OS family.

## [1.0.2] - 2024-06-30

### Role - authentication_proxy

- Added some extra description for the `duoap_configure_firewalld` and `duoap_configure_ufw` variables.

## [1.0.1] - 2024-06-30

### Role - authentication_proxy

- Updated documentation and role metadata for readability.

## [1.0.0] - 2024-06-12

### Collection

- Initial release.
- *authentication_proxy* role added.
