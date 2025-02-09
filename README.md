# ansible-role-base
Base role that can be required by others to ensure the environment is correctly configured (e.g., special user creation)

## Quick Install & Run
```bash
REQ_VESION="feature/base-user-config-role" && REQ_REPO="FoxySimon/ansible-playbook-primary" && ROLE_VERSION="feature/base-user-config-role" && ROLE_REPO="FoxySimon/ansible-playbook-primary" && TMP_FILE=$(mktemp) && curl https://raw.githubusercontent.com/$REQ_REPO/refs/heads/$REQ_VESION/requirements.yaml -o $TMP_FILE.yaml && ansible-galaxy install -fr $TMP_FILE.yaml && ansible-pull -Uhttps://github.com/$ROLE_REPO -fC $ROLE_VERSION local.yml
```
