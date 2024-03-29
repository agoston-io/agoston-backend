# Agoston Backend

The best tech stack for applications.
The reason is simple, it just implements together the best of the open-source world:

- **Postgres:** The World's Most Advanced Open Source Relational Database.
  - **Function:** To build custom logic.
  - **Trigger:** To trigger functions on data changes or events.
  - **pg_cron:** To schedule function execution regularly.
  - **REST requests python package:** to call any REST API.
- **Postgraphile:** Fastest GraphQL API server for PostgreSQL.
- **Passport JS:** Simple authentication for Node.js.
- **Unified Authentication:** User gets a session that works for requests AND subscriptions.
- **Nodemailer:** A module for Node.js applications to allow easy-as-cake email sending.

**NOTE:** Test for free the in the [Agoston cloud](https://agoston.io).

# Repository content

All you need to run your self-hosted Agoston backend: the role
will deploy an Agoston backend with a reverse proxy on the targeted host.

## Support

Shout out your questions on our [Discord server](https://discord.com/channels/1027572174468415620/1027572175139504191).

## Requirements

- Linux server (Tested on Ubuntu 20.04 LTS) with Python 3.
- Ansible (>=2.13) with collections

```bash
sudo apt install python3-pip
python3 -m pip install ansible
ansible-galaxy collection install community.docker
ansible-galaxy collection install community.general
```

# Role Variables

- `backend_domain`: the domain name for the backend server (used for the reverse proxy).
- `ansible_host`: server name/IP on which you want to deploy the Agoston backend.
- `ansible_user`: the server user with the private SSH key authorized on the target server.
This server must be able to become `root` via the proper privilege delegation:

```bash
sudo sh -c 'echo "<ansible_user> ALL=(ALL) NOPASSWD: ALL" >  /etc/sudoers.d/<ansible_user>'

Example with user niolap:
sudo sh -c 'echo "niolap ALL=(ALL) NOPASSWD: ALL" > /etc/sudoers.d/niolap'
```
- All variables in `defaults/main.yml` can be overwritten to fit your environment.

# SSL certificates

The role will generate a self signed certificat. If you wish to use your own,
install them here after the role execution:

```bash
# file /etc/nginx/sites-enabled/default
ssl_certificate /etc/ssl/<backend_domain>.crt;
ssl_certificate_key /etc/ssl/<backend_domain>.key;
```

Then restart nginx:

```bash
systemctl restart nginx
```

# Example Playbook

```bash
# Change directory to the playbook directory
cd ~/agoston-backend/playbooks

# Deploy your Agoston backend
ansible-playbook deploy.yml

# Destroy your backend
ansible-playbook destroy.yml
```

# License

See LiCENSE file.

# Author Information

Nicolas Penot (Agoston.io) - nicolas@agoston.io
