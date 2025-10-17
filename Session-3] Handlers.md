## Easy Level (Conceptual)

1. **What is a handler in Ansible?**  
   → A special task triggered only when notified by another task.

2. **When are handlers typically used?**  
   → To restart or reload services after a configuration change.

3. **Do handlers run if the notifying task makes no changes?**  
   → No, they run only when the task reports a change.

4. **Can multiple tasks notify the same handler?**  
   → Yes, a handler can be triggered by multiple tasks.

5. **When in the play execution do handlers run?**  
   → Handlers run at the end of the play or when triggered.

6. **Can a handler be triggered multiple times?**  
   → No, handlers run once per play, even if notified multiple times.

7. **What YAML section defines handlers?**  
   → The `handlers:` section in a playbook.

8. **Is it mandatory to use handlers in every playbook?**  
   → No, handlers are optional and used for specific scenarios.

9. **Can handlers include variables and templates?**  
   → Yes, handlers can use variables and templates like regular tasks.

10. **Can handlers notify other handlers?**  
    → Yes, handlers can trigger other handlers using `notify`.

## Moderate Level (Technical)

1. **Write a playbook to install Apache and restart it only if a config file changes.**  
   → Use `copy` with `notify: Restart Apache` and define a handler.

2. **How do you prevent a handler from running if a task fails?**  
   → Handlers only run if the notifying task completes successfully.

3. **Can handlers be conditional?**  
   → Yes, using `when` statements.

4. **How can you force a handler to run immediately instead of waiting until the end?**  
   → Use `listen` + `meta: flush_handlers`.

5. **How do you reuse handlers across multiple plays or playbooks?**  
   → Define handlers in separate files and include them with `handlers_files:`.

6. **Can a handler restart multiple services at once?**  
   → Yes, a handler can have multiple tasks.

7. **How do you debug handler execution?**  
   → Use `-v` or `-vvv` when running the playbook to see when handlers are triggered.

8. **Can handlers accept arguments like normal tasks?**  
   → Yes, they can use modules with parameters.

9. **What happens if a task changes a file but no handler is defined?**  
   → The change occurs, but no service will be restarted automatically.

10. **How do you ensure a handler runs before the next task?**  
    → Use `meta: flush_handlers` after the task that triggers it.

## Hard Level (Scenario-Based)

1. **You have multiple web servers and want to restart Nginx only on servers where the config changed. How do you implement this?**  
   → Use `copy` with `notify` on each server; handlers run only where changes occurred.

2. **You need to restart multiple services in a specific order after updates. How would you design handlers?**  
   → Create multiple handlers with dependencies and use `listen` with notify chaining.

3. **A task notifies a handler, but the service is already running with the correct configuration. What happens?**  
   → The handler runs anyway unless `changed_when: false` is specified.

4. **You want to trigger a handler immediately instead of waiting for the end of the play. What approach will you use?**  
   → Use `meta: flush_handlers` after the notifying task.

5. **Multiple tasks notify the same handler, but one fails. Will the handler run?**  
   → Only tasks that succeed trigger the handler.

6. **You want different handlers to run based on host groups. How can you achieve this?**  
   → Use conditional `when: inventory_hostname in group_name` in the handler.

7. **Can a handler perform tasks like sending emails or API calls?**  
   → Yes, handlers can perform any task like regular playbook tasks.

8. **You want to prevent handlers from running if a dry run (`--check`) is executed. How?**  
   → Handlers honor `--check` mode and will not execute any changes.

9. **How do you debug which handler caused a change in a large playbook?**  
   → Run playbook with `-vvv` to see notifications and handler execution.

10. **You have nested playbooks with included roles. How can you trigger a handler defined in a role from a task in the main playbook?**  
    → Use `notify: role_handler_name` and ensure handler is loaded via `handlers/main.yml`.
