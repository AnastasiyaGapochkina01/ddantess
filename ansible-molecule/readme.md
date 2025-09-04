```bash
pip install ansible molecule "molecule-plugins[docker]"
ansible-galaxy init role_name
cd role_name
molecule init scenario --driver-name docker
```
