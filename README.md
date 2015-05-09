Bedrock Site protect
====================

This role is specifically crafted to go with [Bedrock-Ansible](https://github.com/roots/bedrock-ansible). It will allow you to set Basic authentication on your bedrock websites. This is especially useful during development if you have a staging environment that you don't want the world to see.

Requirements
------------

This role is made for Bedrock-Ansible, so it depends on it. 

Role Variables
--------------

The role will read from the `wordpres_sites` dict set in environments files of Bedrock-Ansible. It will search for the `htpasswd` key. Example:

<pre>
wordpress_sites:
  example.com:
    site_hosts:
      - example.dev
    local_path: '../site' # path targeting local Bedrock site directory (relative to Ansible root)
    repo: git@github.com:roots/bedrock.git
    site_install: true
    site_title: Example Site
    admin_user: admin
    admin_password: admin
    admin_email: admin@example.dev    
    multisite:
      enabled: false
      subdomains: false
    <b>htpasswd:
        name: user
        password: secret</b>
    ssl:
      enabled: false
    system_cron: true
    env:
      wp_home: http://example.dev
      wp_siteurl: http://example.dev/wp
      wp_env: development
      db_name: example_dev
      db_user: example_dbuser
      db_password: example_dbpassword
</pre>

You can also set the `htpasswd_path` to specify the folder used to store `htpasswd` files. The default is `/etc/htpasswd`. If you want to set this parameter, it is recommended that you set it in the `group_vars/all` file, so it will be the same for all environments.


Dependencies
------------

[Bedrock-Ansible](https://github.com/roots/bedrock-ansible).

Example Playbook
----------------

Add this role (`louim.bedrock-site-protect`) to the `requirements.yml` file in your Bedrock installation, then re-run the `ansible-galaxy install -r requirements.yml` to install the new role. You might need to add the `-f` option to force install of previously downloaded roles.

You will also need to add the role to the `server.yml` like so: 

```
roles:
  ... other Bedrock roles ...
  - { role: bedrock-site-protect, tags: [wordpress, wordpress-setup] }
```

Follow the example above to get started. if the `htpasswd` key is removed from the environment file, the protection will be removed on the next deploy.

License
-------

MIT

Author Information
------------------

© [Louis-Michel Couture](https://twitter.com/louim) 2015. Role inspired by [ansible-htpasswd](https://github.com/weareinteractive/ansible-htpasswd) by [franklinkim](https://github.com/franklinkim)