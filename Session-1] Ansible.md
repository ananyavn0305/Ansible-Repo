## Easy Level (Conceptual Understanding)

1. **What is Ansible?**  
   → Ansible is an open-source automation tool used for configuration management, application deployment, and orchestration.

2. **What language does Ansible use for automation scripts?**  
   → YAML (Yet Another Markup Language).

3. **What is the control node in Ansible?**  
   → The server where Ansible is installed and from which automation commands are executed.

4. **What are managed nodes?**  
   → The target machines that Ansible controls remotely via SSH or WinRM.

5. **Does Ansible require an agent on managed nodes?**  
   → No, Ansible is agentless and uses SSH or WinRM for communication.

6. **What is the default location of the Ansible inventory file?**  
   → `/etc/ansible/hosts`

7. **What is an Ansible Playbook?**  
   → A YAML file containing a list of tasks for configuration or deployment.

8. **What is an Ansible module?**  
   → A pre-built unit of work (like `apt`, `yum`, `copy`, etc.) used inside playbooks.

9. **What command is used to run a playbook?**  
   → `ansible-playbook playbook.yml`

10. **What does the keyword `become: yes` do in a playbook?**  
    → It runs tasks with elevated (sudo) privileges.

## Moderate Level (Technical + Practical)

1. **Explain the architecture of Ansible.**  
   → It consists of a Control Node, Managed Nodes, Inventory, and Playbooks.

2. **What are the two common inventory file formats in Ansible?**  
   → INI and YAML.

3. **How do you define groups in an inventory file?**  
   → By using square brackets `[group_name]` followed by hostnames/IPs.

4. **How can you use a custom inventory file instead of the default one?**  
   → Use `-i` flag, e.g., `ansible-playbook -i custom_inventory.ini playbook.yml`.

5. **What is the difference between `ansible` and `ansible-playbook` commands?**  
   → `ansible` runs ad-hoc commands, while `ansible-playbook` executes YAML automation scripts.

6. **How do you check Ansible installation version?**  
   → `ansible --version`

7. **How do you ensure a package like Nginx is installed on all web servers?**  
   → By writing a playbook using the `apt` or `yum` module targeting `web_servers`.

8. **What does ‘idempotent’ mean in Ansible context?**  
   → It ensures running a playbook multiple times gives the same result without redoing unchanged tasks.

9. **How can you verify SSH connectivity to managed nodes?**  
   → Using `ansible all -m ping`.

10. **What are facts in Ansible?**  
    → System information automatically gathered from managed nodes using the `setup` module.

## Hard Level (Scenario-Based + Deep Concepts)

1. **You deployed a playbook, but one task failed midway. How can you rerun only failed tasks?**  
   → Use `--limit @/path/to/last_failed.json` or the `--start-at-task` option.

2. **How would you secure credentials used in playbooks?**  
   → By using **Ansible Vault** to encrypt sensitive data.

3. **If a playbook is supposed to install Apache but fails on one node due to permission issues, what will happen?**  
   → Ansible stops on that host (by default), but continues on others unless `ignore_errors: yes` is set.

4. **How do you handle different OS types (Ubuntu/CentOS) in the same playbook?**  
   → Use conditional statements with `when` clauses based on `ansible_os_family`.

5. **How would you roll back changes made by a playbook automatically?**  
   → Implement a handler or rollback task triggered by failure conditions.

6. **What happens if a managed node becomes unreachable during playbook execution?**  
   → Ansible marks it as failed and proceeds with other reachable hosts.

7. **How do you use variables in Ansible playbooks?**  
   → By defining them under `vars:` or by using separate variable files (`vars_files:`).

8. **How can you organize a large Ansible project efficiently?**  
   → By using **roles** — structured directories for tasks, handlers, variables, and templates.

9. **How can you run specific tags in a playbook instead of all tasks?**  
   → Using the `--tags` flag (e.g., `ansible-playbook play.yml --tags "install"`).

10. **You need to deploy Nginx only if it’s not already running. How will you handle this in Ansible?**  
    → Use the `when` condition along with the `service` or `command` module to check service status before installation.
