## Easy Level (Conceptual)

1. **What is Ansible Galaxy?**  
→ It is a community hub for sharing and discovering Ansible roles, collections, and automation content.

2. **Why is Ansible Galaxy useful?**  
→ It provides reusable automation code, saving time and effort in writing playbooks from scratch.

3. **What is an Ansible role?**  
→ A structured way to organize Ansible content (tasks, variables, templates, handlers, etc.) into reusable components.

4. **How do you create a new Ansible role?**  
→ Using the command:  
`ansible-galaxy init role_name`

5. **What command is used to install a role from Ansible Galaxy?**  
→ `ansible-galaxy install role_name`

6. **What is the directory structure of an Ansible role used for?**  
→ It organizes different components like defaults, tasks, handlers, templates, and variables logically.

7. **Where are the default variables stored in a role?**  
→ In the `defaults/main.yml` file.

8. **Where should static files (to be copied to remote hosts) be placed in a role?**  
→ Inside the `files/` directory.

9. **Which file in a role contains the list of tasks to execute?**  
→ `tasks/main.yml`

10. **What is the purpose of the handlers directory in a role?**  
→ It defines handlers that are triggered using `notify` when certain tasks change.

## Moderate Level (Technical)

1. **What is the difference between the defaults and vars directories in a role?**  
→ `defaults/` contains variables with the lowest precedence, while `vars/` contains variables with higher precedence.

2. **What is stored inside the meta/main.yml file?**  
→ Role metadata like author info, dependencies, supported platforms, and version details.

3. **How can you include a role in a playbook?**  
→ By using the `roles:` keyword:  
```yaml
- hosts: localhost
  roles:
    - role_name
```

4. **What does the templates/ directory contain?**  
→ Jinja2 template files that can dynamically generate configuration files based on variables.

5. **How do you ensure that a service like NGINX starts automatically on boot within a role?**  
→ Use the `service` module with `enabled: true`.

6. **Can a role include another role?**  
→ Yes, by defining role dependencies inside `meta/main.yml`.

7. **Where are downloaded roles stored when installed from Ansible Galaxy?**  
→ Typically in `~/.ansible/roles` or the path defined in `ansible.cfg` under `roles_path`.

8. **What is the difference between a playbook and a role?**  
→ A playbook orchestrates the automation process, while a role provides modular and reusable building blocks.

9. **How can you update an existing role downloaded from Ansible Galaxy?**  
→ Using the command:  
`ansible-galaxy install --force role_name`

10. **How can you specify multiple roles in a playbook?**  
→ List them under the `roles:` section, e.g.:  
```yaml
roles:
  - nginx_role
  - mysql_role
```
## Hard Level (Scenario-Based)

1. **You need to install NGINX on multiple servers with a reusable setup. How would you approach it?**  
→ Create a role with `ansible-galaxy init`, add tasks to install and configure NGINX, then include it in multiple playbooks.

2. **How can you make a role reusable for both Ubuntu and CentOS systems?**  
→ Use conditional tasks (`when:`) with OS checks and different package modules (`apt` for Ubuntu, `yum` for CentOS).

3. **You want to use a community role from Ansible Galaxy. How do you ensure it’s compatible with your environment?**  
→ Check the role’s metadata (`meta/main.yml`) for supported platforms and Ansible version compatibility.

4. **Suppose your role depends on another role (like installing NGINX before configuring it). How do you handle that?**  
→ Declare dependencies inside `meta/main.yml`:  
```yaml
dependencies:
  - nginx
```

5. **You have customized a role downloaded from Galaxy. How can you prevent it from being overwritten on updates?**  
→ Clone it into your project’s local `roles/` directory and modify it separately instead of reinstalling.

6. **How can you pass custom variables to a role at runtime?**  
→ Use `vars:` or `-e` (extra vars) in the playbook or command line.  
Example:  
`ansible-playbook play.yml -e "nginx_port=8080"`

7. **What is the best practice for testing a new role locally?**  
→ Use the `ansible-playbook` command with `connection: local` or test in a container using tools like Molecule.

8. **How can you share your custom role with others?**  
→ Publish it to Ansible Galaxy using  
`ansible-galaxy role import <GitHub_user> <repo_name>`.

9. **You want to include tasks conditionally based on a variable inside a role. How would you do it?**  
→ Add a `when:` condition in the role’s `tasks/main.yml`.

10. **What steps would you follow to troubleshoot a role that’s failing to run properly?**  
→ Run the playbook with `-vvv` for verbose output, check syntax using `ansible-lint`, and validate task logic inside the role.
