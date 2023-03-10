Manage system users in Linux
=========

Create, remove or lock users

Requirements
------------

* This role requires ansible 1.9 or higher.
* For create new password run 
  * Linux (**mkpasswd -m SHA-512**)
  * Macos (**openssl3 passwd -6**) ```# My openssl3 version: OpenSSL 3.0.8 7 Feb 2023 (Library: OpenSSL 3.0.8 7 Feb 2023)```
    * **install openssl 3 version:**
      * brew install openssl@3
      * ln -s /opt/homebrew/opt/openssl@3/bin/openssl /usr/local/bin/openssl3
  and change key password: ```$6$xxx...```
  * Default password: **pass**

Role Variables
--------------

```yaml
adduser:
  users:
    - name: username
      pubkey: "{{ lookup('file', '~/.ssh/pubkeys/username.pub') }}"
      groups: users
      change: false
    - name: username1
      pubkey: "ssh-rsa AAAAB3NzaC1yc2EAA... username@hostname"
      change: true
rmuser:
  users:
    - username2
lock:
  users:
    - username3
deploy_user: true
```

Default vars in role:

```yaml
defgroup: users
deploy_user: false
```

Dependencies
------------

None

Example Playbook
----------------

Including an example of how to use your role:

```yaml
- hosts: servers
  become: true
  roles:
     - { role: adduser }
```

License
-------

BSD

Author Information
------------------

Created by [CHIP](https://t.me/CHIP0K)
