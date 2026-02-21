ca_certificates
===============
[![Ansible Lint](https://github.com/oxivanisher/role-ca_certificates/actions/workflows/ansible-lint.yml/badge.svg)](https://github.com/oxivanisher/role-ca_certificates/actions/workflows/ansible-lint.yml)

This role either installs or removes system CA certificates. Currently this role supports SUSE, RedHat, and Debian based distributions.

Role Variables
--------------
| Name                          | Comment                                                      | Default value |
| ----------------------------- | ------------------------------------------------------------ | ------------- |
| ca_certificates_absent        | A list of certificates to be absent.                         | `[]`          |
| ca_certificates_desktop_users | A list of                                                    |               |
| ca_certificates_present       | A list of certificates to be present. See the example below. | `[]`          |

Each element of `ca_certificates_present` needs the following fields:

| Key     | Value                                                                 |
| ------- | --------------------------------------------------------------------- |
| name    | The filename under which the file will be saved on the target system. |
| content | The content of the certificate file. See below for more context.      |

A example would look like this:
```yaml
ca_certificates_absent:
  - ca_cert_filename_a_old
  - ca_cert_filename_d_leaked

ca_certificates_present:
  - name: ca_cert_filename_a
    content: |
      -----BEGIN CERTIFICATE-----
      secret content and such
      such securtity wow==
      -----END CERTIFICATE-----
  - name: ca_cert_filename_b
    content: |
      -----BEGIN CERTIFICATE-----
      secret content and such
      even more securtity wow==
      -----END CERTIFICATE-----
  - name: ca_cert_filename_c
    content: "{{ lookup('file', '~/tmp_files/some_secret_ca_certificate') }}"

```

Example Playbook
----------------

```yaml
- name: Configure system CA certificates
  hosts: desktop
  roles:
    - role: umbag.linux_ops.ca_certificates
```

License
-------

BSD

Author Information
------------------

This role is part of the [oxivanisher.linux_base](https://galaxy.ansible.com/ui/repo/published/oxivanisher/linux_base/) collection, and the source for that is located on [github](https://github.com/oxivanisher/collection-linux_base).
