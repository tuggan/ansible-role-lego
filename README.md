Role Name
=========

Deploy and configure [lego](https://go-acme.github.io/lego/) for certificate requests.

Requirements
------------

None.

Role Variables
--------------

| Variable        | Required | Default       | Description                                                                                               |
| --------------- | -------- | ------------- | --------------------------------------------------------------------------------------------------------- |
| lego_accept_tos | Yes      |               | Accept legos TOS, **will get stuck waiting for TOS acceptance if this is not set**.                       |
| lego_email      | Yes      |               | The email to use for the requests.                                                                        |
| lego_domains    | Yes      |               | List of domains to get certificates for. See table below for options                                      |
| lego_dns        | No       |               | If set, specifies that dns proof should be used, and with what provider.                                  |
| lego_disable_cp | No       |               | Option for enabling the `disable-cp` flag.                                                                |
| lego_env        | No       |               | Dictionary of environment variables to add when running the commands.                                     |
| lego_binary     | No       | /usr/bin/lego | lego binary is location.                                                                                  |
| lego_base_dir   | No       | /etc/lego     | Where the lego binary will be run. The certificates will be available inside `{{ lego_base_dir }}/.lego`. |

## lego_domains

| Name     | Required | Default | Description                           |
| -------- | -------- | ------- | ------------------------------------- |
| domain   | Yes      |         | The domain.                           |
| user     | No       |         | Owner for the certificate files.      |
| group    | No       |         | Group for the certificate files.      |
| privmode | No       |         | File mode for the private key.        |
| pubmode  | No       |         | File mode for the public certificate. |


Dependencies
------------

None.

Example Playbook
----------------

    - hosts: servers
      roles:
         - tuggan.lego
      vars:
        lego_email: 'YOUR EMAIL'
        lego_dns: loopia
        lego_domains:
          - domain: 'YOUR DOMAIN'
            user: root
            group: postfix
            privmode: 0640
            pubmode: 0640
        lego_base_dir: /var/spool/postfix/lego
        lego_disable_cp: true
        lego_env:
          LOOPIA_API_USER: 'YOUR USER'
          LOOPIA_API_PASSWORD: 'YOUR PASSWORD'
        lego_accept_tos: true

License
-------

BSD
