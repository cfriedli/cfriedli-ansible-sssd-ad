# Ansible Role: cfriedli-sssd-ad (for Active Directory)

An ansible role that installs SSSD (for Active Directory) on EL 7 and EL 8.

Requirements
--------------
None

Role Variables
--------------

| Variable Name                            | Description                                                                                                           |
| ---------------------------------------- | ----------------------------------------------------------------------------------------------------------------------|
| `linux_ad_debug_level: ""`               | Default SSSD log level                                                                                                |
| `linux_ad_resolv_domain: ""`             | Name of the AD realm                                                                                                  |
| `linux_ad_resolv_nameservers: []`        | List of Active Directory Domain Services (AD DS)                                                                      |
| `linux_ad_resolv_options: []`            | Option allows certain internal resolver variables to be modified                                                      |
| `linux_ad_resolv_search: []`             | Search list for host-name lookup                                                                                      |
| `linux_ad_resolv_sortlist: []`           | Allows addresses returned by gethostbyname to be sorted                                                               |
| `linux_ad_computer_ou: ""`               | The distinguished name of an organizational unit to create the computer account. <br> The exact format of the distinguished name depends on the client software and membership software. <br> You can usually omit the root DSE portion of distinguished name. This is an Active Directory specific option. <br> This can be the full DN or an RDN, relative to the root entry. The subtree must already exist.                        |
| `linux_ad_accessgroups: []`              | List of access groups                                                                                                 |
| `linux_ad_testgroup: ""`                 | Group used do test the Active Directory membership                                                                    |
| `linux_ad_realm: []`                     | Default Kerberos realm                                                                                                |
| `linux_ad_site: ""`                      | Name of the Active Directory site                                                                                     |
| `linux_ad_user: ""`                      | The user name to be used to authenticate with when joining the machine to the realm.                                  |
| `linux_ad_bind_password: ""`             | Password for the `linux_ad_user`                                                                                      |

For the default values of these variables check the `defaults/main.yml`.

Example Playbook
----------------

     - hosts: all
       vars_fall vars/main.yml
       roles:
      - { role: cfriedli.sssd-ad }
  
Inside vars/main.yml:

      linux_ad_testgroup: "acme"
      linux_ad_debug_level: 2
      linux_ad_realm: "acme.com"
      linux_ad_computer_ou:
        - OU=DEV
        - OU=IT
        - DC=ACME
        - DC=COM
      
      linux_ad_access_groups:
              - coyotes@acme.com
      linux_ad_resolv_nameservers:
              - 8.8.8.8
              - 9.9.9.9
      linux_ad_resolv_search:
              - "{{ linux_ad_realm }}"
      linux_ad_resolv_options:
            - "timeout:2"

License
-------

[GPLv3](https://tldrlegal.com/license/gnu-general-public-license-v3-%28gpl-3%29)


Author Information
------------------

The `cfriedli.sssd-ad` role was written by Christian Friedli | [e-mail](mailto:christian.friedli@id.unibe.ch) | [GitHub](https://github.com/cfriedli)

