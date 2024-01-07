# Server fleet playbooks

I use these playbooks for managing my web server and home servers.

## Playbooks description

### `enroll.plays.yml`

Prepares host for further management with ansible. The pllaybook creates a user called ansible, adds it to the sudoers file with no password required, and inserts SSH key for the user.
