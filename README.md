# ansible-role-base
Base role that can be required by others to ensure the environment is correctly configured for Ansible automation.

## What This Role Does

This role performs several essential setup tasks:

1. **Creates and configures a dedicated Ansible user** with proper permissions
2. **Sets up sudo access** for package management without password prompts
3. **Generates SSH keys** for the Ansible user
4. **Installs and configures SSH daemon** using the willshersystems.sshd dependency

## Dependencies

This role depends on the willshersystems.sshd role for SSH daemon configuration. Dependencies are managed through the `requirements.yml` file.

## OneKnowledge Quick Install & Run
**Note:** This command must be run as root. 

```bash
PLAYBOOK_REPO="FoxySimon/ansible-playbook-primary" && \
PLAYBOOK_VERSION="feature/base-user-config-role" && \
ROLE_REPO="FoxySimon/ansible-role-base" && \
ROLE_VERSION="master" && \
TMP_FILE=$(mktemp) && \
curl -L https://raw.githubusercontent.com/$ROLE_REPO/refs/heads/$ROLE_VERSION/requirements.yml -o $TMP_FILE.yml && \
ansible-galaxy install -fr $TMP_FILE.yml 2>&1 | tee >(logger -t ansible) && \
ansible-pull -U https://github.com/$PLAYBOOK_REPO -fC $PLAYBOOK_VERSION local.yml 2>&1 | tee >(logger -t ansible)
```

## Variables

| Variable | Description | Default |
|----------|-------------|---------|
| base_user | Username for the Ansible user | ansible |
| base_user_create_home | Whether to create a home directory | true |
| base_user_state | User state (present/absent) | present |
| base_groups | Admin groups to add the user to | [sudo, wheel, admin] |
| base_groups_extra | Additional groups to add | [] |
| base_sudo_nopasswd_commands | Commands allowed without password | [/usr/bin/apt, /usr/bin/apt-get, /usr/bin/dnf, /usr/bin/yum] |
