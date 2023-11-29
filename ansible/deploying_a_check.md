# How to deploy a Sensu check

## Prerequisites

- Ensure you have coreutils (required for sha512sum) installed.

## 1. Write your script in the correct format

Sensu expects exit code 0 for success, 1 for warning, and 2 for critical.

## 2. Turn your script into an asset

1. Create a folder for your check in `resources/sensu/custom_assets` folder (e.g. `smartsheet-populate-domains`)
2. Put your check in the folder you created
3. Run the following playbook: `ansible-playbook playbooks/ops-server-sensu.yml --tags assets`

- To upload a single check, you can run the following instead: `ansible-playbook playbooks/ops-server-sensu.yml --tags single_package,proto -e 'single_package=smartsheet'`

## 3. Write your check definition

1. Open up `playbooks/tasks/sensu/checks/main.yml`
2. Add your check definition

```yml
- name: # Name of your check
  tags: checks
  sensu.sensu_go.check:
    name: # Name of your sensu check
    
```

3. Run `ansible-playbook playbooks/ops-server-sensu.yml --tags checks`

You did it!