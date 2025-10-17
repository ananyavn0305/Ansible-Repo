## Easy Level (Conceptual)

**1. What is an inventory file in Ansible?**  
→ A file that lists managed nodes, their IPs/hostnames, and connection details.

**2. Why do we need a keypair for connecting to a remote server?**  
→ To securely authenticate the Ansible control node with the remote server over SSH.

**3. What is the purpose of `chmod 400 keypair.pem`?**  
→ It sets the private key permissions so only the owner can read it, securing SSH access.

**4. What does `become: true` do in a playbook?**  
→ It runs tasks with elevated privileges (sudo).

**5. What is the difference between `apt` and `yum` modules in Ansible?**  
→ `apt` is used for Debian-based distributions, while `yum` is for RedHat-based distributions.

**6. What is the purpose of `gather_facts: true`?**  
→ It collects system information from remote hosts into `ansible_facts` for conditional tasks.

**7. Why do we use the `service` module in a playbook?**  
→ To manage services (start, stop, enable, disable) on remote servers.

**8. What is a playbook in Ansible?**  
→ A YAML file containing a series of tasks and instructions to automate operations on remote hosts.

**9. How do you specify the remote user in an inventory file?**  
→ Using `ansible_user=your_ssh_user` in the host entry.

**10. Can Ansible manage multiple remote servers at once?**  
→ Yes, by grouping them in the inventory file and targeting the group in the playbook.

## Moderate Level (Technical)

**1. How do you copy a keypair to a remote server from your control node?**  
→ Using `scp -i ansible_keypair.pem localpath user@remote_ip:destination`.

**2. Write a simple playbook to install Nginx on a Debian-based server.**  
→ Use `apt` module with `state: present` and `update_cache: true`.

**3. How do you handle different Linux distributions in a single playbook?**  
→ Use `when` conditions with `ansible_os_family` or `ansible_facts['distribution']`.

**4. How can you ensure a service is enabled on boot using Ansible?**  
→ By setting `enabled: yes` in the `service` module.

**5. What does `update_cache: true` do in the apt module?**  
→ Updates the package database before installing the package.

**6. How do you connect to a remote host using a non-default SSH key?**  
→ Specify `ansible_private_key_file=keypair.pem` in the inventory file.

**7. Explain the difference between `hosts: webservers` and `hosts: all`.**  
→ `webservers` targets a specific group in the inventory, `all` targets all hosts.

**8. How do you conditionally run tasks on Ubuntu but not on Amazon Linux?**  
→ Using `when: ansible_facts['distribution'] == "Ubuntu"`.

**9. What happens if a task fails on one server when running against multiple servers?**  
→ By default, the play continues on other hosts unless `any_errors_fatal` or `ignore_errors` is used.

**10. How do you verify that Nginx is running after installation?**  
→ Use the `service` module with `state: started` and `enabled: yes`, or check using Ansible ad-hoc commands.

## Hard Level (Scenario-Based)

**1. You have multiple remote servers with different OS. How would you install Nginx on all of them with one playbook?**  
→ Use conditional tasks with `ansible_os_family` or `ansible_facts['distribution']` and the appropriate package module (`apt`/`yum`).

**2. Your keypair permissions are too open (e.g., 644). What problem might occur?**  
→ SSH will refuse to use the key due to insecure permissions, causing connection failure.

**3. You want to run a playbook on only Ubuntu servers in a group containing mixed OS. How would you do it?**  
→ Use `when: ansible_facts['distribution'] == "Ubuntu"` on tasks or create a separate group for Ubuntu in inventory.

**4. A server fails to install Nginx using the apt module due to locked dpkg. How do you handle this in Ansible?**  
→ Use `apt: force: yes` or include a pre-task to unlock the package manager.

**5. How would you automate service installation and ensure it’s restarted if the config file changes?**  
→ Use `notify` to trigger a handler after copying the configuration file.

**6. You need to connect to a remote server behind a bastion host. How can you achieve this?**  
→ Use `ansible_ssh_common_args='-o ProxyJump=user@bastion'` in the inventory.

**7. You want to run a command on multiple servers but only gather facts once. How would you implement it?**  
→ Set `gather_facts: false` in the playbook and use ad-hoc `setup` module on one host if needed.

**8. How would you structure a playbook to support future package additions for multiple OS?**  
→ Use loops (`with_items` or `loop`) with conditional OS checks.

**9. You have multiple tasks that depend on Nginx being installed. How do you ensure task order?**  
→ Place tasks sequentially in the playbook; Ansible executes tasks in order defined.

**10. Your playbook runs successfully, but Nginx is not enabled on reboot for some servers. What might be wrong?**  
→ `enabled: yes` might be missing in the `service` module, or OS-specific differences may prevent auto-start.
