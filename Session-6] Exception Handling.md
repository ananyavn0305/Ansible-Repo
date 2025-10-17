## Easy Level (Conceptual)

**1. What is exception handling in Ansible?**  
→ It refers to managing errors or unexpected conditions during playbook execution using structured blocks like `block`, `rescue`, and `always`.

**2. Why is exception handling important in automation?**  
→ It prevents playbook failures from stopping the automation process and allows recovery or alternative actions.

**3. What are the three main sections used for error handling in Ansible?**  
→ `block`, `rescue`, and `always`.

**4. What is the role of the `block` section in Ansible?**  
→ It contains the main set of tasks that are attempted first (like a “try” block in programming).

**5. When does the `rescue` section execute?**  
→ It runs only when a task inside the `block` section fails.

**6. What is the function of the `always` section?**  
→ It always runs — whether the block succeeds or fails — typically used for cleanup or status reporting.

**7. Can you have multiple tasks under `block`, `rescue`, and `always` sections?**  
→ Yes, each section can contain multiple tasks.

**8. Does every block need a `rescue` or `always` section?**  
→ No, both are optional — you can use only `block`, or combine as needed.

**9. What happens if both the `block` and `rescue` sections fail?**  
→ The playbook will stop execution unless error ignoring (`ignore_errors`) is explicitly used.

**10. Which directive in Ansible is equivalent to a “finally” block in programming languages like Python?**  
→ The `always` section.

## Moderate Level (Technical)

**1. What happens in the example when Ansible tries to install the package `dgjskja`?**  
→ It will fail (since it’s invalid), and the control will move to the `rescue` block.

**2. What does the `rescue` block do in the given playbook example?**  
→ It installs Nginx as an alternative and prints a message using the debug module.

**3. What is the purpose of the `debug` module in this playbook?**  
→ It displays custom messages to indicate which section (`block`, `rescue`, `always`) is being executed.

**4. Can you nest `block`, `rescue`, and `always` structures in Ansible?**  
→ Yes, nested blocks are supported for complex error-handling logic.

**5. What is the advantage of using `block` and `rescue` instead of `ignore_errors: yes`?**  
→ `block` and `rescue` allow structured recovery actions instead of just skipping failed tasks.

**6. If the `block` succeeds, will the `rescue` block still execute?**  
→ No, `rescue` executes only when a task inside `block` fails.

**7. Will the `always` block run even if the playbook fails in both `block` and `rescue`?**  
→ Yes, the `always` block runs regardless of the outcome.

**8. How can you ensure a cleanup task always runs, even if errors occur?**  
→ Place the cleanup task under the `always` section.

**9. How can you combine exception handling with conditional execution?**  
→ By using `when` clauses inside `block`, `rescue`, or `always` sections.

**10. What does the `become: true` statement do in this playbook?**  
→ It ensures that all tasks run with elevated privileges (sudo).

## Hard Level (Scenario-Based)

**1. Suppose the Nginx installation in the `rescue` block also fails. How would you handle it?**  
→ Use another nested `block` with its own `rescue`, or use `ignore_errors: yes` with proper logging in `always`.

**2. How can you send a notification (email or Slack message) when an error occurs in the `block`?**  
→ Include a notification task in the `rescue` section using appropriate modules like `mail` or `slack`.

**3. If you want to rollback configuration changes after a failed deployment, where should you place rollback tasks?**  
→ Inside the `rescue` section.

**4. You want to log all playbook failures regardless of success or failure. Where should you place the logging task?**  
→ Inside the `always` section.

**5. How would you handle different error types differently inside a single playbook?**  
→ Use conditional checks (`when` clauses) in the `rescue` block based on the failed task or its result.

**6. Can you run cleanup steps even if the playbook is stopped using Ctrl+C?**  
→ Not always — `always` executes within Ansible’s normal error-handling flow but won’t run if execution is forcefully terminated.

**7. How can you test if your `rescue` block is working correctly?**  
→ Intentionally make a task fail (e.g., install an invalid package) to trigger the rescue logic.

**8. If a playbook includes multiple blocks, how does Ansible handle them when one fails?**  
→ Each block is independent; only the failed block triggers its associated `rescue` and `always`.

**9. What is the difference between `block` and `pre_tasks` in Ansible?**  
→ `block` is for error-handling logic within a play, while `pre_tasks` run before all other tasks and aren’t tied to block logic.

**10. How would you extend this example to include a post-cleanup step like restarting a service only if installation succeeds?**  
→ Use a conditional task after the block or place it in `always` with a condition such as `when: result is succeeded`.
