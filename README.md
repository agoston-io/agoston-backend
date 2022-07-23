# Agoston Backend

All you need to run your self-hosted Agoston backend.

## Requirements

- Linux server (Tested on Ubuntu 20.04 LTS) with Python 3.
- Ansible with collections

```bash
sudo apt install python3-pip
python3 -m pip install ansible
ansible-galaxy collection install community.docker
```

# Role Variables

- `ansible_host`: server name/IP on which you want to deploy the Agoston backend.
- `ansible_user`: the server user with the private SSH key authorized on the target server.
This server must be able to become `root` via the proper privilege delegation:

```bash
sudo sh -c 'echo "<ansible_user> ALL=(ALL) NOPASSWD: ALL" >  /etc/sudoers.d/<ansible_user>'

Example with user niolap:
sudo sh -c 'echo "niolap ALL=(ALL) NOPASSWD: ALL" > /etc/sudoers.d/niolap'
```

# Example Playbook

```bash
# Change directory to the playbook directory
cd ~/agoston-backend/playbooks

# Run the deployment of Agoston backend
ansible-playbook deploy.yml \
-e ansible_host=agoston-backend \
-e ansible_user=niolap
```

# License

See LiCENSE file.

# Author Information

Nicolas Penot (Agoston.io) - nicolas@agoston.io
