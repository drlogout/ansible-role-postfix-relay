ansible-role-postfix-relay
==========================

This ansible role installs postfix as a relay server. 

All mail send from this host will have the same from address.

Role Variables
--------------

Required variables:

```yml

# SMTP credentials
#postfix_relay_smtp_host: "" (required)
postfix_relay_smtp_port: 587
#postfix_relay_smtp_user: "" (required, must be an email address)
#postfix_relay_smtp_password: "" (required)

postfix_relay_hostname: "{{ inventory_hostname }}"

# Rewrite local receipients
postfix_relay_receipient_mappings: []

# Who should receive root's email?
#postfix_relay_root_forward: user@example.com (required)

# Additional users whose email should be forwarded to postfix_relay_root_forward
postfix_relay_forward_aliases: []

# Skip installation if e.g. running inside a docker container at runtime
postfix_relay_skip_install: false

```

Example Playbook
----------------

**vars file:**

```yml

postfix_relay_smtp_host: mail.example.com
postfix_relay_smtp_user: server1@example.com
postfix_relay_smtp_password: alskdfhlqiufqjgdjqd

postfix_relay_root_forward: admin@example.com

postfix_relay_receipient_mappings:
  - { src: "@{{ inventory_hostname_short }}", dest: "@{{ inventory_hostname }}" }
  - { src: "@localhost", dest: "@{{ inventory_hostname }}" }
  - { src: "root", dest: "root@{{ inventory_hostname }}" }


```

**playbook:**

```yml

    - hosts: servers
      roles:
         - ansible-role-postfix-relay

```

License
-------

BSD
