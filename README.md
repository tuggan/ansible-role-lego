Role Name
=========

Deploy and configure [lego](https://go-acme.github.io/lego/) for certificate requests.

Requirements
------------

None.

Role Variables
--------------

 - `lego_accept_tos`: Accept legos TOS, **will get stuck waiting for TOS acceptance if this is not set**.
 - `lego_binary`: Where the lego binary is located.
 - `lego_base_dir`: Where the lego binary will be run. The certificates will be available inside `{{ lego_base_dir }}/.lego`.
 - `lego_email`: The email to use for the requests.
 - `lego_dns`: If set, specifies that dns proof should be used, and with what provider.
 - `lego_domains`: List of domains to get certificates for.
   - `domain`: The domain.
   - `user`: Owner for the certificate files.
   - `group`: Group for the certificate files.
   - `privmode`: File mode for the private key.
   - `pubmode`: File mode for the public certificate.
 - `lego_disable_cp`: Option for enabling the `disable-cp` flag.
 - `lego_env`: Dictionary of environment variables to add when running the commands.


Dependencies
------------

None.

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

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
