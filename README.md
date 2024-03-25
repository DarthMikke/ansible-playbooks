# Server fleet playbooks

I use these playbooks for managing my web server and home servers.

## Playbooks description

### [`enroll.plays.yml`](playbooks/enroll.plays.yml)

Prepares host for further management with ansible. The pllaybook creates a user called ansible, adds it to the sudoers file with no password required, and inserts SSH key for the user.

### [`ssl.plays.yml`](playbooks/ssl.plays.yml)

Generate SSL certs with Let's Encrypt as provider and Linode as DNS registrar.

#### vars

`credentials`:
- path to [credentials file](https://certbot-dns-linode.readthedocs.io/en/stable/#credentials) with Linode token giving DNS write access.
- default value: `"../linode-credentials.ini"`

`cert_groups`:
- host groups, as defined in hosts inventory file.
- for every host in these groups, two variables must be defined:
    - `ssl_domains`, a set of domains its SSL certificate will be valid for, comma separated. E.g.: `example.com,www.example.com,blog.example.com`.
    - `ssl_main_domain`, being the domain Certbot uses as the directory name
    where the certificate is stored. Usually it is the first of the domains in
    `ssl_domains`, in the example above: `example.com`.
- default value:
```yml
  - web
  - vpn_servers
```

### [`new-project.plays.yml`](playbooks/new-project.plays.yml)

For a project called `homepage` ensure that:
1. a `www-homepage` user exists and is accessible from the current node;
2. a `homepage` directory exists in the server root directory.
