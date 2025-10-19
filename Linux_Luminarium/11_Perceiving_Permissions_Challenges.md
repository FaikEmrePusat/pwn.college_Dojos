# Perceiving Permissions
<p>This module will expose you to Linux permissions, which is one of the most important parts of your journey going ahead, and mediates the access to files across different users.</p>
<p>In Linux, files have different permissions or file modes.
You can check out the permissions of a file or directory using <code>ls -l</code>.
Let's make some files and look at their permissions:</p>
<pre><code class="language-console hljs shell">hacker@dojo:~$ mkdir pwn_directory
hacker@dojo:~$ touch college_file
hacker@dojo:~$ ls -l
total 4
-rw-r--r-- 1 hacker hacker    0 May 22 13:42 college_file
drwxr-xr-x 2 hacker hacker 4096 May 22 13:42 pwn_directory
hacker@dojo:~$
</code></pre>
<p>Lots of information there, and we'll learn about a lot of it in this module!
For now, let's look at the output above at a high level:</p>
<h4>The File Type</h4>
<p>The first character of each line represents the file type.
In <code>pwn_directory</code>'s case, the <code>d</code> indicates that it's a directory, and in <code>college_file</code>'s case, the <code>-</code> represents that it's a normal file.
There are other types as well, and you will encounter some of them later in your pwn.college journey.</p>
<h4>The Permissions</h4>
<p>The next nine characters are the actual access permissions of the file or directory, split into 3 characters denoting the permissions that the user who owns the file (termed the "owner") has to the file, 3 characters denoting the permissions that the group that owns the file (termed the "group") has to the file, and 3 characters denoting the permissions that all other access (e.g., by other users and other groups) has to the file.
We will learn all about these later in the module.</p>
<h4>Ownership Information</h4>
<p>There are two columns showing the <em>user</em> that owns the file (in this case, user <code>hacker</code>) and then the <em>group</em> that owns the file (in this case, also group <code>hacker</code>).
You'll mess around with that here!</p>

<p>In this module, you will practice perceiving permissions.
Let's get started!</p>

---

## Changing File Ownership
To complete this challenge, you need to change the ownership of the `/flag` file to the `hacker` user using the `chown` command, then read the flag. Here are the steps:

1. Change the ownership of `/flag` to `hacker`:
   ```bash
   chown hacker /flag
   ```

2. Read the flag:
   ```bash
   cat /flag
   ```

This will output the flag for the challenge. Note that in this specific challenge, you are allowed to use `chown` as the `hacker` user without needing root privileges.

---

## Groups and Files
### Challenge Description
Change the group ownership of the `/flag` file to the `hacker` group using `chgrp`, then read the flag.

### Concepts Learned
- **Group Ownership**: Files can be owned by both a user and a group  
- **`chgrp` command**: Changes the group ownership of files and directories  
- **Group-based Permissions**: Access to files can be controlled through group membership  

### Steps to Get the Flag
1. **Change the group ownership of `/flag` to `hacker`**:  
   ```bash
   chgrp hacker /flag
   ```  

2. **Read the flag**:  
   ```bash
   cat /flag
   ```  

**Note**  
- The `/flag` file initially has permissions `-r--r-----`, meaning only the owner (root) and group (root) can read it  
- After changing the group to `hacker`, members of the `hacker` group (including your user) can read the file  
- This demonstrates how group ownership controls file access in Linux

---

## Fun With Groups Names
To complete this challenge, you need to determine your group name using the `id` command, then change the group ownership of the `/flag` file to that group using `chgrp`. Finally, read the flag.

### Steps:
1. **Find your group name**:
   ```bash
   id
   ```
   Look for the `gid` or `groups` field in the output. For example, if the output is `uid=1000(hacker) gid=1000(mygroup) groups=1000(mygroup)`, then your group name is `mygroup`.

2. **Change the group ownership of `/flag` to your group**:
   ```bash
   chgrp mygroup /flag
   ```
   Replace `mygroup` with the actual group name from step 1.

3. **Read the flag**:
   ```bash
   cat /flag
   ```

This will output the flag for the challenge. The key is using `id` to discover your randomized group name and then applying it with `chgrp`.

---

## Changing Permissions
### Challenge Description
Use the `chmod` command to modify the permissions of the `/flag` file, making it readable by your user, then read the flag.

### Concepts Learned
- **File Permissions**: Control read (r), write (w), and execute (x) access for user, group, and others  
- **`chmod` command**: Changes file permissions using symbolic (e.g., `u+r`) or numeric modes  
- **Permission Modification**: Adding or removing specific permissions for different access classes  

### Steps to Get the Flag
1. **Add read permission for others on `/flag`**:  
   ```bash
   chmod o+r /flag
   ```  
   This adds read permission for all users (others) to the flag file.

2. **Read the flag**:  
   ```bash
   cat /flag
   ```  

**Note**  
- The original permissions are `-r--------` (only root can read)  
- After `chmod o+r`, permissions become `-r-----r--` (root and all other users can read)  
- This demonstrates how file permissions control access independently of ownership

---

## Executable Files
### Challenge Description
Use the `chmod` command to add execute permissions to the `/challenge/run` program, then execute it to receive the flag.

### Concepts Learned
- **Execute Permissions**: Required to run programs as executable files  
- **`chmod` command**: Modifies file permissions using symbolic notation  
- **Program Execution**: Linux requires execute permission to run programs directly  

### Steps to Get the Flag
1. **Add execute permission to `/challenge/run`**:  
   ```bash
   chmod +x /challenge/run
   ```  
   This adds execute permission for all users (user, group, and others).

2. **Run the program**:  
   ```bash
   /challenge/run
   ```  

**Note**  
- The `+x` syntax is shorthand for adding execute permission to all categories  
- You could be more specific with `u+x` (user only), `g+x` (group only), or `o+x` (others only)  
- This demonstrates how execute permissions control whether files can be run as programs

---

## Permission Tweaking Practice
### Challenge Description
Complete eight consecutive permission changes on `/challenge/pwn` as instructed by the interactive challenge, then modify `/flag` permissions to read it.

### Concepts Learned
- **`chmod` command**: Modifies file permissions using symbolic (e.g., `u=rwx,g=rx,o=r`) or octal (e.g., `754`) modes  
- **File Permissions**: Control read (r), write (w), and execute (x) access for user, group, and others  

### Steps to Get the Flag
1. **Start the interactive challenge**:  
   ```bash
   /challenge/run
   ```  

2. **Follow the prompts to change `/challenge/pwn` permissions eight times**:  
   - Use `chmod` with the specified permissions for each round  
   - Example formats:  
     ```bash
     chmod u=rwx,g=rx,o=r /challenge/pwn    # Symbolic mode
     chmod 754 /challenge/pwn                # Octal mode
     ```  

3. **After eight successful changes, make `/flag` readable**:  
   ```bash
   chmod o+r /flag
   ```  

4. **Read the flag**:  
   ```bash
   cat /flag
   ```  

**Note**  
- The challenge resets if any permission change is incorrect  
- Use `ls -l /challenge/pwn` to verify permissions between changes  
- This demonstrates precise permission management using `chmod`

---

## Permissions Setting Practice
To complete this challenge, you need to interactively change the permissions of the `/challenge/pwn` file eight times in a row as specified by the challenge program. After each correct change, the program will prompt you for the next set of permissions. Once all eight changes are correct, you will be able to modify the permissions of `/flag` to read it.

### Steps:
1. **Start the challenge**:
   ```bash
   /challenge/run
   ```

2. **Follow the prompts and change permissions using `chmod`**:
   - Use the `chmod` command with symbolic modes to set the exact permissions requested.
   - Example formats based on the requirements:
     ```bash
     chmod u=rwx,g=rx,o= /challenge/pwn    # Set user to rwx, group to rx, others to nothing
     chmod u=rw,g=r,o=r /challenge/pwn      # Set user to rw, group to r, others to r
     chmod a=rx,u=w /challenge/pwn          # Set all to rx, but user to w (overrides user)
     ```
   - After each `chmod` command, verify the permissions with `ls -l /challenge/pwn` if needed, but the challenge will inform you if the permissions are correct.

3. **After eight successful changes, make `/flag` readable**:
   ```bash
   chmod o+r /flag
   ```
   or use the method instructed by the challenge.

4. **Read the flag**:
   ```bash
   cat /flag
   ```

### Important Notes:
- The challenge uses symbolic modes with `=` to set permissions exactly. You can chain multiple changes with commas (e.g., `u=rwx,g=rx,o=`).
- If you make a mistake, the challenge will reset, and you must start over.
- The specific permissions for each round will be provided by the challenge program. Pay close attention to the requirements.

This exercise reinforces precise control over file permissions using `chmod` with symbolic modes. Good luck!

---

## The SUID Bit
### Challenge Description
Set the SUID bit on `/challenge/getroot` using `chmod`, then execute it to spawn a root shell and read the flag.

### Concepts Learned
- **SUID (Set User ID)**: Special permission that allows a program to run with the privileges of the file owner  
- **Privilege Escalation**: Using SUID binaries to gain higher privileges  
- **Root Shell**: A shell running with root privileges that can access protected files  

### Steps to Get the Flag
1. **Add the SUID bit to `/challenge/getroot`**:  
   ```bash
   chmod u+s /challenge/getroot
   ```  
   This sets the SUID bit, so the program runs as root regardless of who executes it.

2. **Execute the program to get a root shell**:  
   ```bash
   /challenge/getroot
   ```  
   This will spawn a shell with root privileges.

3. **Read the flag**:  
   ```bash
   cat /flag
   ```  

**Note**  
- Verify the SUID bit is set with `ls -l /challenge/getroot` (should show `-rwsr-xr-x`)  
- The program must be owned by root for SUID to provide root privileges  
- This demonstrates how SUID binaries can be used for legitimate privilege escalation
