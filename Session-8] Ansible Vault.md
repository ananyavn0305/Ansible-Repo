## Easy Level (Conceptual)

1. **What is Ansible Vault used for?**  
→ It is used to encrypt and protect sensitive data such as passwords, API keys, and certificates in Ansible files.

2. **Why is Ansible Vault important in automation?**  
→ It prevents sensitive information from being exposed in version control or logs.

3. **Which command is used to encrypt a file in Ansible?**  
→ `ansible-vault encrypt filename.yml`

4. **Which command decrypts an encrypted file?**  
→ `ansible-vault decrypt filename.yml`

5. **What kind of data can you store in an encrypted Ansible Vault file?**  
→ Passwords, API keys, tokens, certificates, and other confidential variables.

6. **What file extension is typically used for vault files?**  
→ `.yml` (though any extension can be used).

7. **How do you include a vault file in a playbook?**  
→ Using the `vars_files:` directive.

8. **When running an encrypted playbook, how do you provide the decryption password?**  
→ By using the `--ask-vault-pass` option.

9. **Can Ansible Vault be used to encrypt only parts of a file?**  
→ Yes, with `ansible-vault encrypt_string` to encrypt individual variables.

10. **Is Ansible Vault encryption symmetric or asymmetric?**  
→ It uses symmetric encryption (same password for encrypting and decrypting).

## Moderate Level (Technical)

1. **What does the command `ansible-vault encrypt mypass.yml` do?**  
→ It encrypts the contents of the `mypass.yml` file using a password prompt.

2. **What happens if you try to read an encrypted file without decrypting it?**  
→ You’ll see scrambled text (ciphertext) and won’t be able to read its contents.

3. **How do you run a playbook that includes an encrypted variable file?**  
→ `ansible-playbook playbook.yml --ask-vault-pass`

4. **What is the purpose of the `vars_files` keyword in the playbook?**  
→ It allows including external files containing variables, including encrypted ones.

5. **How does Ansible access variables from an encrypted file during execution?**  
→ It decrypts them in memory when the correct vault password is provided.

6. **How do you change the password of an existing encrypted file?**  
→ Using `ansible-vault rekey filename.yml`

7. **What module in the playbook uses the credentials from `mypass.yml`?**  
→ The `community.mysql.mysql_user` module.

8. **How do you avoid entering the vault password manually every time?**  
→ By using a `--vault-password-file` that contains the password or script to return it.

9. **What does the `--ask-vault-pass` option do during playbook execution?**  
→ Prompts the user to enter the vault password to decrypt files.

10. **Can multiple vaults with different passwords be used in a single playbook?**  
→ Yes, by tagging each file with a unique vault ID and password source.

## Hard Level (Scenario-Based)

1. **Suppose your vault password is lost — can you decrypt the file?**  
→ No, decryption is impossible without the correct password.

2. **How would you securely share a playbook with encrypted variables to a team?**  
→ Share the encrypted files and separately communicate the vault password securely.

3. **You need to update a single variable inside an encrypted file. How can you do it without decrypting everything manually?**  
→ Use `ansible-vault edit filename.yml` which decrypts temporarily for editing and re-encrypts on save.

4. **You want to encrypt only the password variable inside a file, not the whole file. How can you do that?**  
→ Use `ansible-vault encrypt_string 'password123' --name 'db_pass'`.

5. **What would happen if you forget to pass the vault password while running the playbook?**  
→ Ansible will throw an error saying it cannot decrypt the encrypted variables.

6. **How can you run an encrypted playbook automatically in a CI/CD pipeline?**  
→ Use a vault password file (`--vault-password-file`) stored securely in the pipeline’s secrets manager.

7. **You have multiple environment files (dev, test, prod) with different secrets. How do you manage them efficiently?**  
→ Create separate vault-encrypted files for each environment and reference them dynamically in the playbook.

8. **How can you verify that a file is encrypted with Ansible Vault?**  
→ The file begins with the line `$ANSIBLE_VAULT;1.1;AES256`.

9. **Suppose your playbook fails due to a vault decryption error — how would you troubleshoot it?**  
→ Check if the correct password was used and ensure the vault version and syntax are valid.

10. **You want to rotate vault passwords across multiple encrypted files. How can you automate this?**  
→ Use a script with `ansible-vault rekey` to systematically update passwords for all vault files.
