# How to deploy a Sensu check

## 1. Write your script in the correct format

Sensu expects exit code 0 for success, 1 for warning, and 2 for critical.

## 2. Turn your script into an asset

1. Put your check in the `custom_assets` folder
2. Run the following playbook: `ansible-playbook playbooks/ops-server-sensu.yml --tags assets`

## 3. Write your check definition

1. Open up `tasks/sensu/checks/main.yml`
2. Add your check definition (TODO: add example code with comments below)
3. Run `ansible-playbook playbooks/ops-server-sensu.yml --tags checks`

You did it!