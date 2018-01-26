haproxy-tls
=========

This role will configure two haproxy nodes in an active-passive configuration on DigitalOcean Droplets. The provided TLS certificate will be configured on the haproxy nodes for TLS termination.

Requirements
------------

A TLS certificate is required along with the private key in one file. Please use ansible-vault to keep your data safe.

Role Variables
--------------

A description of the settable variables for this role should go here, including any variables that are in defaults/main.yml, vars/main.yml, and any variables that can/should be set via parameters to the role. Any variables that are read from other roles and/or the global scope (ie. hostvars, group vars, etc.) should be mentioned here as well.

I recommend setting the *do_token* and *ha_auth_key* variables in **group_vars/*group_name*** and setting them to the values stored in an ansible-vault encrypted file in **group_vars/all/vault**

    # DigitalOcean access token
    do_token: "{{ vault_do_token }}"

    # Generated ha auth key.
    ha_auth_key: "{{ vault_ha_auth_key }}"

Just don't forget to set *vault_do_token* and *vault_ha_auth_key*.

You can adjust the following two variables in defaults/main.yml

    timezone: "America/Los_Angeles"
    locale: "en_US.UTF-8"

You'll also want to place your encrypted TLS certificate in **files/cert.pem**.


Example usage
----------------

You should install the role before attempting to execute directly from a playbook since you'll need to place your cert.pem file in the role's **files** directory.

    ansible-galaxy install -r requirements.yml

or

    ansible-galaxy install cmndrsp0ck.haproxy-tls

Once the role is installed you can set it up in your playbook.

    - hosts: load_balancer
      roles:
          - { role: haproxy-tls }
      become: True

License
-------

BSD
