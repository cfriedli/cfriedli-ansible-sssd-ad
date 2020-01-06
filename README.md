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

      linux_ad_join_admin: !vault |                                                                                          
                $ANSIBLE_VAULT;1.1;AES256                                                                                    
                30316461356631636161663264326262386463313430613154543545432542432424366536646462                             
                3839663237363266354324235435234141633035636330310a363264643636646639303062643334                             
                33366439393430643636373763666265643243423432565641666138376435316461373936643632                             
                3431633038353264350a613430623261633632323833306534336130363862623335306632656464                             
                6539                                                                                                         
      linux_ad_bind_password: !vault |                                                                                       
                $ANSIBLE_VAULT;1.1;AES256                                                                                    
                36636230303334616235613565653065316330356643242342303838383262633536303734363638
                3833364234234235543625613761326262303063303832620a432432424354354365716338646662                             
                32323030633032393636546456547654323423546333653633336461343263613634383136373039                             
                3230376633633833380a653232613737616362365464765452341234234235363166653933616262
                3364                 
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


Author Information
------------------

The `cfriedli.sssd-ad` role was written by Christian Friedli | [e-mail](mailto:christian.friedli@id.unibe.ch) | [GitHub](https://github.com/cfriedli)

