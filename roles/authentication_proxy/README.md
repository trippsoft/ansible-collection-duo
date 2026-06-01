<!-- BEGIN_ANSIBLE_DOCS -->

# Ansible Role: trippsc2.duo.authentication_proxy
Version: 1.1.0

This role installs and configures a DUO Authentication Proxy on a Linux machine.

## Requirements

| Platform | Versions |
| -------- | -------- |
| Debian | <ul><li>bookworm</li></ul> |
| EL | <ul><li>9</li><li>8</li></ul> |
| Ubuntu | <ul><li>noble</li><li>jammy</li></ul> |

## Dependencies

| Collection |
| ---------- |
| ansible.posix |
| ansible.utils |
| community.general |

## Role Arguments
|Option|Description|Type|Required|Choices|Default|
|---|---|---|---|---|---|
| duoap_configure_selinux | <p>Whether the role will configure SELinux for the DUO Authentication Proxy.</p> | bool | no |  | True |
| duoap_configure_logrotate | <p>Whether the role will configure logrotate for the DUO Authentication Proxy.</p> | bool | no |  | True |
| duoap_configure_firewall | <p>Whether the role will configure the host firewall for use with DUO Authentication Proxy.</p> | bool | no |  | True |
| duoap_user | <p>The Linux user as which the DUO Authentication Proxy will run.</p> | str | no |  | duo_authproxy_svc |
| duoap_group | <p>The Linux primary group of the *duoap_user* user.</p> | str | no |  | duo_authproxy_grp |
| duoap_install_path | <p>The path of the symlink to the currently installed DUO Authentication Proxy version.</p><p>The installed version will be placed in a folder at path suffixed with `-<version>`.</p> | path | no |  | /opt/duoauthproxy |
| duoap_version | <p>The version of the DUO Authentication Proxy to install.</p><p>If not specified, the latest version will be installed.</p><p>If another version is already installed and *duoap_upgrade* is set to `false`, this is ignored.</p> | str | no |  |  |
| duoap_upgrade | <p>Whether the role will upgrade or downgrade the DUO Authentication Proxy.</p><p>If set to `false` and any version of DUO Authentication Proxy is installed, the role will not install another version.</p><p>If set to `true`, *duoap_version* is not specified, and a version other than the latest is installed, the role will upgrade to the latest version.</p><p>If set to `true`, *duoap_version* is specified, and a version other than that version is installed, the role will upgrade or downgrade to the specified version.</p> | bool | no |  | False |
| duoap_temp_path | <p>The path where temporary files will be stored during the installation process.</p> | path | no |  | /tmp/duoap |
| duoap_cleanup_old_version | <p>Whether the role will remove old versions of the DUO Authentication Proxy after upgrading or downgrading.</p> | bool | no |  | False |
| duoap_service_account_username | <p>The default service user account that the DUO Authentication Proxy will use to authenticate with Active Directory.</p> | str | no |  |  |
| duoap_service_account_password | <p>The password for the *duoap_service_account_username* user account.</p> | str | no |  |  |
| duoap_api_host | <p>The FQDN of the DUO API server.</p> | str | no |  |  |
| duoap_log_dir | <p>The directory where DUO Authentication Proxy logs will be stored.</p><p>See: https://duo.com/docs/authproxy-reference#main-section</p> | path | no |  | /var/log/duo |
| duoap_debug | <p>Whether DUO Authentication Proxy will run in debug mode.</p><p>See: https://duo.com/docs/authproxy-reference#main-section</p> | bool | no |  | False |
| duoap_log_auth_events | <p>Whether DUO Authentication Proxy will log authentication events.</p><p>See: https://duo.com/docs/authproxy-reference#main-section</p> | bool | no |  | False |
| duoap_log_sso_events | <p>Whether DUO Authentication Proxy will log SSO events.</p><p>See: https://duo.com/docs/authproxy-reference#main-section</p> | bool | no |  | False |
| duoap_log_max_files | <p>The maximum number of log files to keep.</p><p>If set to `0`, all log files will be kept.</p><p>If *duoap_configure_logrotate* is `true`, this will default to `0`.</p><p>Otherwise, this will default to `6`.</p><p>See: https://duo.com/docs/authproxy-reference#main-section</p> | int | no |  |  |
| duoap_log_max_size_in_mb | <p>The maximum size of each log file in megabytes before the logs will be rotated by the DUO Authentication Proxy.</p><p>If set to `0`, the log files will not be rotated.</p><p>If *duoap_configure_logrotate* is `true`, this will default to `0`.</p><p>Otherwise, this will default to `10`.</p><p>See: https://duo.com/docs/authproxy-reference#main-section</p> | int | no |  | 10 |
| duoap_http_ca_certs_file | <p>The path to a file containing CA certificates to trust when making HTTP requests.</p><p>For Debian-based systems, this will default to `/etc/ssl/certs/ca-certificates.crt`.</p><p>For EL systems, this will default to `/etc/pki/tls/certs/ca-bundle.crt`.</p><p>See: https://duo.com/docs/authproxy-reference#main-section</p> | path | no |  |  |
| duoap_interface | <p>The IP address on which the DUO Authentication Proxy will listen.</p><p>If not specified, DUO Authentication Proxy will listen on all interface addresses.</p><p>See: https://duo.com/docs/authproxy-reference#main-section</p> | str | no |  |  |
| duoap_http_proxy_host | <p>The hostname of the HTTP proxy server.</p><p>See: https://duo.com/docs/authproxy-reference#main-section</p> | str | no |  |  |
| duoap_http_proxy_port | <p>The port of the HTTP proxy server.</p><p>See: https://duo.com/docs/authproxy-reference#main-section</p> | int | no |  |  |
| duoap_test_connectivity_on_startup | <p>Whether the DUO Authentication Proxy will test connectivity to the DUO API server on startup.</p><p>See: https://duo.com/docs/authproxy-reference#main-section</p> | bool | no |  | False |
| duoap_fips_mode | <p>Whether the DUO Authentication Proxy will run in FIPS mode.</p><p>See: https://duo.com/docs/authproxy-reference#main-section</p> | bool | no |  | False |
| duoap_ad_clients | <p>A list of Active Directory clients.</p><p>See: https://duo.com/docs/authproxy-reference#ad_client</p> | list of dicts of 'duoap_ad_clients' options | no |  | [] |
| duoap_radius_clients | <p>A list of RADIUS clients.</p><p>See: https://duo.com/docs/authproxy-reference#radius_client</p> | list of dicts of 'duoap_radius_clients' options | no |  | [] |
| duoap_duo_only_client_enabled | <p>Whether the DUO Authentication Proxy will only allow DUO authentication.</p> | bool | no |  | False |
| duoap_ldap_auto_servers | <p>A list of LDAP auto servers.</p><p>See: https://duo.com/docs/authproxy-reference#ldap-auto</p> | list of dicts of 'duoap_ldap_auto_servers' options | no |  | [] |
| duoap_radius_auto_servers | <p>A list of RADIUS auto servers.</p><p>See: https://duo.com/docs/authproxy-reference#radius-auto</p> | list of dicts of 'duoap_radius_auto_servers' options | no |  | [] |
| duoap_dirsync_clouds | <p>Whether the role will configure directory synchronization.</p><p>See: https://duo.com/docs/authproxy-reference#cloud-section</p> | list of dicts of 'duoap_dirsync_clouds' options | no |  | [] |
| duoap_configure_sso | <p>Whether the role will configure SSO.</p><p>See: https://duo.com/docs/authproxy-reference#sso-section</p> | bool | no |  | False |
| duoap_sso_remote_identity_key | <p>The SSO remote identity key.</p><p>If *duoap_configure_sso* is `false`, this variable is ignored.</p><p>Otherwise, it is required.</p><p>See: https://duo.com/docs/authproxy-reference#sso-section</p> | str | no |  |  |
| duoap_sso_service_account_username | <p>The service user account that the DUO Authentication Proxy will use to authenticate with Active Directory.</p><p>If not specified, this will default to the value of *duoap_service_account_username*.</p><p>See: https://duo.com/docs/authproxy-reference#sso-section</p> | str | no |  |  |
| duoap_sso_service_account_password | <p>The password of the *duoap_sso_service_account_username* user account.</p><p>If not specified, this will default to the value of *duoap_service_account_password*.</p><p>See: https://duo.com/docs/authproxy-reference#sso-section</p> | str | no |  |  |
| duoap_logrotate_period | <p>The period at which the logrotate service will rotate DUO log files.</p><p>If *duoap_configure_logrotate* is `false`, this is ignored.</p> | str | no | <ul><li>daily</li><li>weekly</li><li>monthly</li></ul> | daily |
| duoap_logrotate_retention | <p>The number of log files for the logrotate service to retain.</p><p>If *duoap_configure_logrotate* is `false`, this is ignored.</p> | int | no |  | 7 |
| duoap_firewall_type | <p>The type of firewall to configure.</p><p>For Debian or EL systems, this will default to `firewalld`.</p><p>For Ubuntu systems, this will default to `ufw`.</p> | str | no | <ul><li>firewalld</li><li>ufw</li></ul> |  |

### Options for duoap_ad_clients
|Option|Description|Type|Required|Choices|Default|
|---|---|---|---|---|---|
| comment | <p>A comment with which to mark the Active Directory client section.</p> | str | no |  |  |
| hosts | <p>A list of hostnames or IP addresses of Domain Controllers to which to connect.</p><p>See: https://duo.com/docs/authproxy-reference#ad_client</p> | list of 'str' | yes |  |  |
| service_account_username | <p>The service user account that the DUO Authentication Proxy will use to authenticate with Active Directory.</p><p>If not specified, this will default to value of *duoap_service_account_username*.</p><p>See: https://duo.com/docs/authproxy-reference#ad_client</p> | str | no |  |  |
| service_account_password | <p>The password of the *service_account_username* user account.</p><p>If not specified, this will default to value of *duoap_service_account_password*.</p><p>See: https://duo.com/docs/authproxy-reference#ad_client</p> | str | no |  |  |
| search_dn | <p>The LDAP distinguished name of the search base.</p><p>See: https://duo.com/docs/authproxy-reference#ad_client</p> | str | yes |  |  |
| security_group_dn | <p>The distinguished name of the security group of which membership is required to login.</p><p>If not specified, no security group will be required.</p><p>See: https://duo.com/docs/authproxy-reference#ad_client</p> | str | no |  |  |
| ldap_filter | <p>An LDAP filter that the users must match to login.</p><p>See: https://duo.com/docs/authproxy-reference#ad_client</p> | str | no |  |  |
| transport | <p>The transport protocol to use when connecting to Active Directory LDAP.</p><p>See: https://duo.com/docs/authproxy-reference#ad_client</p> | str | no | <ul><li>clear</li><li>ldaps</li><li>starttls</li></ul> |  |
| timeout | <p>The timeout in seconds for the connection before failing over to the next host.</p><p>If not specified, DUO Authentication Proxy will default to 10 seconds.</p><p>See: https://duo.com/docs/authproxy-reference#ad_client</p> | int | no |  |  |
| ssl_ca_certs_file | <p>The path to a file containing CA certificates to trust when making SSL connections.</p><p>If not specified, the role will use the system default.</p><p>See: https://duo.com/docs/authproxy-reference#ad_client</p> | path | no |  |  |
| ssl_verify_hostname | <p>Whether to verify the hostname of the SSL certificate.</p><p>See: https://duo.com/docs/authproxy-reference#ad_client</p> | bool | no |  | True |
| auth_type | <p>The authentication type to use.</p><p>If not specified, the role will use `ntlm2`.</p><p>See: https://duo.com/docs/authproxy-reference#ad_client</p> | str | no | <ul><li>ntlm2</li><li>plain</li></ul> |  |
| bind_dn | <p>The distinguished name of the service account that the DUO Authentication Proxy will use to authenticate with Active Directory.</p><p>See: https://duo.com/docs/authproxy-reference#ad_client</p> | str | no |  |  |
| ntlm_domain | <p>The domain to use for NTLM authentication.</p><p>If *auth_type* is `plain`, this will be ignored.</p><p>See: https://duo.com/docs/authproxy-reference#ad_client</p> | str | no |  |  |
| ntlm_workstation | <p>The workstation to use for NTLM authentication.</p><p>If *auth_type* is `plain`, this will be ignored.</p><p>See: https://duo.com/docs/authproxy-reference#ad_client</p> | str | no |  |  |
| port | <p>The port on which to connect.</p><p>See: https://duo.com/docs/authproxy-reference#ad_client</p> | int | no |  |  |
| username_attribute | <p>The attribute to use as the username.</p><p>If not specified, the role will use `sAMAccountName`.</p><p>See: https://duo.com/docs/authproxy-reference#ad_client</p> | str | no |  |  |
| at_attribute | <p>The attribute to use to match usernames with `@` symbol.</p><p>If not specified, the role will use `userPrincipalName`.</p><p>See: https://duo.com/docs/authproxy-reference#ad_client</p> | str | no |  |  |

### Options for duoap_radius_clients
|Option|Description|Type|Required|Choices|Default|
|---|---|---|---|---|---|
| comment | <p>A comment with which to mark the RADIUS client.</p> | str | no |  |  |
| servers | <p>A list of RADIUS servers to which to connect.</p><p>See: https://duo.com/docs/authproxy-reference#radius_client</p> | list of dicts of 'servers' options | yes |  |  |
| secret | <p>The shared secret to use for authentication.</p><p>See: https://duo.com/docs/authproxy-reference#radius_client</p> | str | yes |  |  |
| retries | <p>The number of times to retry connecting to the RADIUS server.</p><p>If not specified, DUO Authentication Proxy will default to 3.</p><p>See: https://duo.com/docs/authproxy-reference#radius_client</p> | int | no |  |  |
| retry_wait | <p>The number of seconds to wait between retries.</p><p>If not specified, DUO Authentication Proxy will default to 2.</p><p>See: https://duo.com/docs/authproxy-reference#radius_client</p> | int | no |  |  |
| nas_ip | <p>The IP address to provide to the RADIUS server as the `NAS-IP-Address` attribute.</p><p>See: https://duo.com/docs/authproxy-reference#radius_client</p> | str | no |  |  |
| pass_through_attr_names | <p>A list of attributes to pass through to the RADIUS server.</p><p>See: https://duo.com/docs/authproxy-reference#radius_client</p> | list of 'str' | no |  |  |
| pw_codec | <p>The codec to use for the password.</p><p>See: https://duo.com/docs/authproxy-reference#radius_client</p> | str | no |  |  |

### Options for duoap_radius_clients > servers
|Option|Description|Type|Required|Choices|Default|
|---|---|---|---|---|---|
| host | <p>The hostname or IP address of the RADIUS server.</p><p>See: https://duo.com/docs/authproxy-reference#radius_client</p> | str | yes |  |  |
| port | <p>The port on which to connect.</p><p>If not specified, DUO Authentication Proxy will default to `1812`.</p><p>See: https://duo.com/docs/authproxy-reference#radius_client</p> | int | no |  |  |

### Options for duoap_ldap_auto_servers
|Option|Description|Type|Required|Choices|Default|
|---|---|---|---|---|---|
| comment | <p>A comment with which to mark the LDAP auto server.</p> | str | no |  |  |
| ikey | <p>The integration key for the DUO Authentication Proxy.</p><p>See: https://duo.com/docs/authproxy-reference#ldap-auto</p> | str | yes |  |  |
| skey | <p>The secret key for the DUO Authentication Proxy.</p><p>See: https://duo.com/docs/authproxy-reference#ldap-auto</p> | str | yes |  |  |
| api_host | <p>The FQDN of the DUO API server.</p><p>See: https://duo.com/docs/authproxy-reference#ldap-auto</p> | str | yes |  |  |
| client | <p>The client ID for the DUO Authentication Proxy.</p><p>See: https://duo.com/docs/authproxy-reference#ldap-auto</p> | str | yes |  |  |
| factors | <p>A list of factors to use for authentication.</p><p>See: https://duo.com/docs/authproxy-reference#ldap-auto</p> | list of 'str' | no | <ul><li>auto</li><li>push</li><li>phone</li><li>passcode</li></ul> |  |
| failmode | <p>The failmode to use for authentication.</p><p>See: https://duo.com/docs/authproxy-reference#ldap-auto</p> | str | no | <ul><li>safe</li><li>secure</li></ul> |  |
| port | <p>The port on which to listen for LDAP.</p><p>If not specified, DUO Authentication Proxy will default to `389`.</p><p>See: https://duo.com/docs/authproxy-reference#ldap-auto</p> | int | no |  |  |
| interface | <p>The network interface on which to listen for LDAP.</p><p>See: https://duo.com/docs/authproxy-reference#ldap-auto</p> | str | no |  |  |
| api_timeout | <p>The timeout in seconds for the API connection.</p><p>If set to `0`, there is no timeout.</p><p>If not specified, this defaults to `0`.</p><p>See: https://duo.com/docs/authproxy-reference#ldap-auto</p> | int | no |  |  |
| network_timeout | <p>The timeout in seconds for the network connection.</p><p>If not specified, the role will default to 10 minutes (600).</p><p>See: https://duo.com/docs/authproxy-reference#ldap-auto</p> | int | no |  |  |
| idle_timeout | <p>The timeout in seconds for the idle connection.</p><p>If not specified, the role will default to 1 hour (3600).</p><p>See: https://duo.com/docs/authproxy-reference#ldap-auto</p> | int | no |  |  |
| ssl_port | <p>The port on which to listen for SSL.</p><p>See: https://duo.com/docs/authproxy-reference#ldap-auto</p> | int | no |  |  |
| ssl_key_path | <p>The path to the SSL key file.</p><p>See: https://duo.com/docs/authproxy-reference#ldap-auto</p> | path | no |  |  |
| ssl_cert_path | <p>The path to the SSL certificate file.</p><p>See: https://duo.com/docs/authproxy-reference#ldap-auto</p> | path | no |  |  |
| exempt_primary_bind | <p>Whether to exempt the primary bind from DUO authentication.</p><p>See: https://duo.com/docs/authproxy-reference#ldap-auto</p> | bool | no |  |  |
| exempt_ous | <p>A list of OUs to exempt from DUO authentication.</p><p>See: https://duo.com/docs/authproxy-reference#ldap-auto</p> | list of 'str' | no |  |  |
| delimiter | <p>The delimiter to separate the password and the passcode in the password field.</p><p>If not specified, the role will default to `,`.</p><p>See: https://duo.com/docs/authproxy-reference#ldap-auto</p> | str | no |  |  |
| delimiter_password_length | <p>The length of the password in the password field.</p><p>All characters after this length will be considered the passcode.</p><p>See: https://duo.com/docs/authproxy-reference#ldap-auto</p> | int | no |  |  |
| allow_concat | <p>Whether to allow concatenation of the password and passcode.</p><p>See: https://duo.com/docs/authproxy-reference#ldap-auto</p> | bool | no |  |  |
| allow_searches_after_bind | <p>Whether to allow searches after the primary bind.</p><p>See: https://duo.com/docs/authproxy-reference#ldap-auto</p> | bool | no |  |  |
| allow_unlimited_binds | <p>Whether to allow unlimited binds.</p><p>See: https://duo.com/docs/authproxy-reference#ldap-auto</p> | bool | no |  |  |
| minimum_tls_version | <p>The minimum TLS version to accept.</p><p>See: https://duo.com/docs/authproxy-reference#ldap-auto</p> | str | no | <ul><li>ssl3</li><li>tls1.0</li><li>tls1.1</li><li>tls1.2</li></ul> |  |
| cipher_list | <p>The list of ciphers to accept.</p><p>These are in OpenSSL format. https://www.openssl.org/docs/man1.1.1/man1/ciphers.html#CIPHER-LIST-FORMAT</p><p>See: https://duo.com/docs/authproxy-reference#ldap-auto</p> | str | no |  |  |

### Options for duoap_radius_auto_servers
|Option|Description|Type|Required|Choices|Default|
|---|---|---|---|---|---|
| comment | <p>A comment with which to mark the RADIUS auto server.</p> | str | no |  |  |
| ikey | <p>The integration key for the DUO Authentication Proxy.</p><p>See: https://duo.com/docs/authproxy-reference#radius-auto</p> | str | yes |  |  |
| skey | <p>The secret key for the DUO Authentication Proxy.</p><p>See: https://duo.com/docs/authproxy-reference#radius-auto</p> | str | yes |  |  |
| api_host | <p>The FQDN of the DUO API server.</p><p>See: https://duo.com/docs/authproxy-reference#radius-auto</p> | str | yes |  |  |
| client | <p>The client ID for the DUO Authentication Proxy.</p><p>See: https://duo.com/docs/authproxy-reference#radius-auto</p> | str | yes |  |  |
| radius_clients | <p>A list of RADIUS clients to use.</p><p>See: https://duo.com/docs/authproxy-reference#radius-auto</p> | list of dicts of 'radius_clients' options | yes |  |  |
| factors | <p>A list of factors to use for authentication.</p><p>See: https://duo.com/docs/authproxy-reference#radius-auto</p> | list of 'str' | no | <ul><li>auto</li><li>push</li><li>phone</li><li>passcode</li></ul> |  |
| delimiter | <p>The delimiter to separate the password and the passcode in the password field.</p><p>If not specified, the role will default to `,`.</p><p>See: https://duo.com/docs/authproxy-reference#radius-auto</p> | str | no |  |  |
| delimiter_password_length | <p>The length of the password in the password field.</p><p>All characters after this length will be considered the passcode.</p><p>See: https://duo.com/docs/authproxy-reference#radius-auto</p> | int | no |  |  |
| allow_concat | <p>Whether to allow concatenation of the password and passcode.</p><p>See: https://duo.com/docs/authproxy-reference#radius-auto</p> | bool | no |  |  |
| api_timeout | <p>The timeout in seconds for the API connection.</p><p>If set to `0`, there is no timeout.</p><p>If not specified, DUO Authentication Proxy defaults to `0`.</p><p>See: https://duo.com/docs/authproxy-reference#radius-auto</p> | int | no |  |  |
| failmode | <p>The failmode to use for authentication.</p><p>See: https://duo.com/docs/authproxy-reference#radius-auto</p> | str | no | <ul><li>safe</li><li>secure</li></ul> |  |
| port | <p>The port on which to listen for RADIUS.</p><p>If not specified, DUO Authentication Proxy will default to `1812`.</p><p>See: https://duo.com/docs/authproxy-reference#radius-auto</p> | int | no |  |  |
| interface | <p>The network interface on which to listen for LDAP.</p><p>See: https://duo.com/docs/authproxy-reference#radius-auto</p> | str | no |  |  |
| pass_through_attr_names | <p>A list of attributes to pass through to the RADIUS server.</p><p>If not specified, DUO Authentication Proxy will pass through no attributes.</p><p>See: https://duo.com/docs/authproxy-reference#radius-auto</p> | list of 'str' | no |  |  |
| pass_through_all | <p>Whether to pass through all attributes to the RADIUS server.</p><p>If not specified, DUO Authentication Proxy will pass through no attributes.</p><p>See: https://duo.com/docs/authproxy-reference#radius-auto</p> | bool | no |  |  |
| client_ip_attr | <p>The attribute to use for the client IP address.</p><p>See: https://duo.com/docs/authproxy-reference#radius-auto</p> | str | no |  |  |
| exempt_usernames | <p>A list of usernames to exempt from DUO authentication.</p><p>See: https://duo.com/docs/authproxy-reference#radius-auto</p> | list of 'str' | no |  |  |
| pw_codec | <p>The codec to use for the password.</p><p>If not specified, DUO Authentication Proxy will default to `UTF-8`.</p><p>See: https://duo.com/docs/authproxy-reference#radius-auto</p> | str | no |  |  |

### Options for duoap_radius_auto_servers > radius_clients
|Option|Description|Type|Required|Choices|Default|
|---|---|---|---|---|---|
| ip | <p>The IP address of the RADIUS client.</p><p>See: https://duo.com/docs/authproxy-reference#radius-auto</p> | str | yes |  |  |
| secret | <p>The shared secret to use for authentication.</p><p>See: https://duo.com/docs/authproxy-reference#radius-auto</p> | str | yes |  |  |

### Options for duoap_dirsync_clouds
|Option|Description|Type|Required|Choices|Default|
|---|---|---|---|---|---|
| comment | <p>A comment with which to mark the directory sync cloud.</p> | str | no |  |  |
| ikey | <p>The integration key for directory synchronization.</p><p>See: https://duo.com/docs/authproxy-reference#cloud-section</p> | str | yes |  |  |
| skey | <p>The secret key for directory synchronization.</p><p>See: https://duo.com/docs/authproxy-reference#cloud-section</p> | str | yes |  |  |
| api_host | <p>The FQDN of the DUO API server for directory synchronization.</p><p>If not specified, this will default to the value of *duoap_api_host*.</p><p>See: https://duo.com/docs/authproxy-reference#cloud-section</p> | str | no |  |  |
| service_account_username | <p>The service user account that the DUO Authentication Proxy will use to authenticate with Active Directory.</p><p>If not specified, this will default to the value of *duoap_service_account_username*.</p><p>See: https://duo.com/docs/authproxy-reference#cloud-section</p> | str | no |  |  |
| service_account_password | <p>The password of the *service_account_username* user account.</p><p>If not specified, this will default to the value of *duoap_service_account_password*.</p><p>See: https://duo.com/docs/authproxy-reference#cloud-section</p> | str | no |  |  |


## License
MIT

## Author and Project Information
Jim Tarpley (@trippsc2)
<!-- END_ANSIBLE_DOCS -->
