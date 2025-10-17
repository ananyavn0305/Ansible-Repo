## Easy Level (Conceptual Understanding)

1. **What is the purpose of `with_items` in Ansible?**  
   → It is used to loop through a list of items and perform a task for each item.

2. **What is the difference between `loop` and `with_items`?**  
   → Both perform loops, but `loop` is the modern syntax recommended over `with_items`.

3. **What module is used to create files and directories in Ansible?**  
   → The `file` module.

4. **Which module is used to copy files from the control node to managed nodes?**  
   → The `copy` module.

5. **What does `state: directory` do in the `file` module?**  
   → It ensures that the given path is a directory.

6. **What does `state: touch` do in the `file` module?**  
   → It creates an empty file if it doesn’t already exist.

7. **What is the role of `mode` in the `file` module?**  
   → It sets file or directory permissions using octal values (e.g., `0755`).

8. **Where does the `src` parameter in the `copy` module point to?**  
   → It refers to the file’s location on the control (Ansible) node.

9. **What does `dest` in the `copy` module specify?**  
   → The destination path on the remote (managed) machine.

10. **What is the benefit of using loops in Ansible?**  
    → Loops simplify repetitive tasks and reduce redundant code.

## Moderate Level (Technical + Practical)

1. **Write an example playbook that installs multiple packages using a loop.**  
   → Use the `apt` module with `loop: ['nginx', 'php', 'mariadb-server']`.

2. **How can you create multiple directories dynamically in Ansible?**  
   → By looping over directory paths with the `file` module and `state: directory`.

3. **If you want to set different permissions for different files, how can you achieve that?**  
   → Use a loop with a dictionary list (list of dictionaries) specifying `path` and `mode`.

4. **Can you use variables inside loops?**  
   → Yes, variables can be used within loops for dynamic item values.

5. **What will happen if the file already exists when using `state: touch`?**  
   → Ansible does nothing; it ensures the file exists (idempotent behavior).

6. **How do you copy multiple configuration files to different destinations?**  
   → Use a loop with the `copy` module, providing a list of dictionaries for `src` and `dest`.

7. **What happens if the `src` file in a `copy` task doesn’t exist?**  
   → The playbook fails for that task with an error.

8. **How can you create both files and directories in a single playbook?**  
   → Combine multiple `file` tasks with `state: directory` and `state: touch`.

9. **What is the use of `become: yes` in file and copy tasks?**  
   → It ensures the tasks run with elevated privileges (e.g., when writing to system paths).

10. **How can you copy an entire directory recursively using the `copy` module?**  
    → By using `copy: src=/path/to/folder dest=/remote/path/ recursive=yes`.
    
## Hard Level (Scenario-Based + Deep Concepts)

1. **You need to install multiple packages on different groups of servers with specific versions. How would you structure the playbook?**  
   → Use conditional loops (`when` with `loop`) and variables defined per host or group.

2. **How can you copy different configuration files to different servers dynamically?**  
   → Use host-specific variables or templates combined with `copy` and a loop.

3. **How would you ensure file creation happens only if a directory exists?**  
   → Use a `when` condition with `ansible.builtin.stat` to check the directory before running the `file` task.

4. **You need to deploy configuration files only if they have changed. How would Ansible handle this automatically?**  
   → The `copy` module automatically checks file differences and reports changes (idempotent behavior).

5. **How can you combine a loop with the `notify` feature in Ansible to restart a service after installing multiple packages?**  
   → Add a handler (e.g., restart Nginx) and trigger it using `notify` inside a looped task.

6. **What happens if one item in a loop fails? Can you skip it and continue?**  
   → Yes, by adding `ignore_errors: yes` or using `rescue` blocks.

7. **You need to create multiple files with specific owners, groups, and permissions. How would you handle this efficiently?**  
   → Use a loop with dictionaries specifying `path`, `owner`, `group`, and `mode`.

8. **How can you perform a dry run to test file or copy tasks without making actual changes?**  
   → Run the playbook with `--check` mode.

9. **You must copy a file from one managed node to another. Can the `copy` module do this directly?**  
   → No, it copies only from control node → managed node. You’d need to use `fetch` + `copy` or the `synchronize` module.

10. **You want to create a directory structure dynamically based on an external YAML file. How will you achieve this?**  
    → Load the YAML file as a variable and loop through its list of directory paths using the `file` module.
