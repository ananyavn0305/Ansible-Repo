## Easy Level (Conceptual)

**1. What are variables in Ansible?**  
→ Variables are used to store reusable values that can be referenced throughout playbooks and templates.

**2. Why are variables important in Ansible?**  
→ They make playbooks dynamic, reusable, and easier to maintain by avoiding hardcoding values.

**3. How do you define variables inside a playbook?**  
→ Using the `vars:` section under a play definition.

**4. What is the syntax for referencing a variable in Ansible?**  
→ Variables are referenced using double curly braces — `{{ variable_name }}`.

**5. What is the purpose of the `template` module in Ansible?**  
→ It is used to copy Jinja2 template files from the control node to managed hosts, replacing variables dynamically.

**6. What does the `file` module do in Ansible?**  
→ It manages files and directories (create, delete, change permissions, etc.) on remote hosts.

**7. Why do we use quotes around variables like `{{ my_path }}`?**  
→ To ensure correct parsing by YAML and Jinja2, especially when paths or strings contain special characters.

**8. What is the difference between the `copy` and `template` modules?**  
→ `copy` copies static files, while `template` processes Jinja2 templates and replaces variables before copying.

**9. Where can variables be defined in Ansible?**  
→ In playbooks, inventory files, variable files, host/group vars, roles, or passed as extra-vars at runtime.

**10. Can Ansible variables contain both numbers and strings?**  
→ Yes, variables can store any data type — strings, integers, lists, dictionaries, etc.

## Moderate Level (Technical)

**1. How can you pass a variable value dynamically during playbook execution?**  
→ By using `--extra-vars` (or `-e`) flag:  
`ansible-playbook myplay.yml -e "my_port=8080"`

**2. What is the use of the following line in a playbook?**  
`path: "{{ my_path }}"`  
→ It dynamically substitutes the directory path from the variable `my_path`.

**3. What is the difference between defining variables inside `vars:` vs. inventory file?**  
→ `vars:` defines variables specific to that play, while inventory variables apply to specific hosts or groups globally.

**4. How would you make a variable available to multiple playbooks?**  
→ By defining it in a separate variable file or inside `group_vars/` or `host_vars/` directories.

**5. In the example, why is `my_port` defined even though it’s not directly used in tasks?**  
→ It could be referenced in the Nginx configuration template (`mynginx.conf`) to dynamically assign a port.

**6. What module is used to reload the Nginx service?**  
→ The `service` module with `state: reloaded`.

**7. How would you handle default values for variables that might not be defined?**  
→ Using Jinja2 syntax with `default` filter: `{{ variable_name | default('value') }}`.

**8. Can you override variables defined in a playbook?**  
→ Yes, variables passed at runtime or from inventory/group_vars take higher precedence.

**9. Why is `connection: local` used in this playbook?**  
→ To run tasks locally on the control node instead of remote managed hosts.

**10. What does `become: true` achieve in this context?**  
→ It runs all tasks with elevated (sudo) privileges.

## Hard Level (Scenario-Based)

**1. Suppose you want to deploy multiple websites using the same playbook but different paths and ports. How would you modify this playbook?**  
→ Define variables (`my_port`, `my_path`) per host or use variable files, then reference them dynamically in tasks and templates.

**2. How can you avoid hardcoding the Nginx path in the playbook?**  
→ Use a variable (e.g., `nginx_conf_path`) and define it in the vars section or external file.

**3. If you run this playbook without defining `my_path`, what will happen?**  
→ The playbook will fail with an undefined variable error unless a default value is provided.

**4. You want to copy a file only if the variable `my_path` exists. How can you do this?**  
→ Use a conditional statement:  
```yaml
when: my_path is defined
```

**5. How can you use the same index.html for multiple servers with different content?**  
→ Create a Jinja2 template file (`index.html.j2`) and use variables for dynamic content.

**6. You want to reuse this playbook for installing Apache instead of Nginx. What changes are required?**  
→ Replace all Nginx-specific package names and service tasks with Apache equivalents and update templates accordingly.

**7. If you define `my_port` in both playbook and inventory, which one will take precedence?**  
→ The value from the inventory file (or host/group vars) will override the playbook value.

**8. How can you debug the value of a variable during playbook execution?**  
→ Use the `debug` module:  
```yaml
- name: Print variable
  debug:
    var: my_path
```

**9. You have different environments (dev, test, prod) — each with unique variables. How can you structure this efficiently?**  
→ Use separate variable files (`vars_dev.yml`, `vars_test.yml`, etc.) and include them dynamically using `vars_files`.

**10. The playbook fails due to permission issues when creating a directory. How can you fix it?**  
→ Ensure `become: true` is set or define proper ownership/permissions in the `file` module using `owner`, `group`, and `mode`.
