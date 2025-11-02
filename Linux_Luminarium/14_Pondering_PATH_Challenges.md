# Pondering PATH
<p>Thus far, you have invoked commands in several ways:</p>
<ul>
<li>Through an absolute path (e.g., <code>/challenge/run</code>).</li>
<li>Through a relative path (e.g., <code>./run</code>).</li>
<li>Through a bare command name (e.g., <code>ls</code>).</li>
</ul>
<p>The first two cases, the absolute and the relative path case, are straightforward: the <code>run</code> file lives in the <code>/challenge</code> directory, and both cases refer to it (provided, of course, that the relative path is invoked with a current working directory of <code>/challenge</code>).
But what about the last one?
Where is the <code>ls</code> program located?
How does the shell know to search for it there?</p>
<p>In this module, we will pull back the veil and answer this question!
Stay with us.</p>

---

## The PATH Variable
### Challenge Description
Disrupt the `/challenge/run` program by modifying the `PATH` environment variable so it cannot find the `rm` command, preventing it from deleting the flag.

### Concepts Learned
- **PATH Variable**: Controls where the shell looks for executable programs  
- **Environment Inheritance**: Child processes inherit environment variables from the parent shell  
- **Command Disruption**: Removing critical commands from PATH can prevent program functionality  

### Steps to Get the Flag
1. **Clear the PATH variable for the challenge program**:  
   ```bash
   PATH="" /challenge/run
   ```  
   This runs the program with an empty PATH, making it unable to find the `rm` command.

2. **The program will fail to delete the flag and will output it instead**

**Alternative Approach**  
You can also export an empty PATH temporarily:  
```bash
export PATH=""
/challenge/run
export PATH="/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin"  # Restore PATH
```

**Note**  
- If the flag gets deleted, restart the challenge and try again  
- This demonstrates how environment variables affect program execution and can be used for security controls

---

## Setting PATH
### Challenge Description
Set the `PATH` environment variable to include `/challenge/more_commands/` so that the `win` command can be found and executed by `/challenge/run`.

### Concepts Learned
- **PATH Modification**: Adding directories to PATH makes their executables accessible by name  
- **Temporary PATH Changes**: Setting PATH for a single command execution  
- **Command Discovery**: How the shell locates programs when given bare command names  

### Steps to Get the Flag
1. **Run the challenge with the modified PATH**:  
   ```bash
   PATH=/challenge/more_commands /challenge/run
   ```  
   This temporarily sets PATH to only include `/challenge/more_commands/` for this command execution.

2. **The program will successfully find and execute the `win` command, outputting the flag**

**Alternative Approach**  
You can also append to the existing PATH:  
```bash
PATH=$PATH:/challenge/more_commands /challenge/run
```

**Note**  
- Setting PATH to just one directory removes access to all standard system commands  
- This demonstrates how to make custom commands available without using their full paths  
- The change only affects the specific command execution, not your entire shell session

---

## Finding Commands
To complete this challenge, you need to find the location of the `win` command using `which`, then navigate to its directory and read the flag file. Here's how:

### Steps:
1. **Find the path to `win`**:
   ```bash
   which win
   ```
   This will output the full path to the `win` command, for example: `/challenge/more_commands/win`.

2. **Change to the directory containing `win`**:
   ```bash
   cd /challenge/more_commands
   ```
   Replace `/challenge/more_commands` with the actual path from step 1.

3. **List the files in the directory** to find the flag file:
   ```bash
   ls
   ```
   You should see a file named `flag` or similar.

4. **Read the flag file**:
   ```bash
   cat flag
   ```
   This will output the flag.

### Note:
- If you cannot change directories, you can directly read the flag by constructing the path. For example, if `which win` returns `/challenge/more_commands/win`, then you can run:
  ```bash
  cat /challenge/more_commands/flag
  ```
- The flag file is readable by you, so no special permissions are needed.

By following these steps, you will retrieve the flag from the directory containing the `win` command.

---

## Adding Commands
### Challenge Description
Create a custom `win` shell script that reads the flag, add its directory to the `PATH`, and run `/challenge/run` so it can find and execute your `win` command.

### Concepts Learned
- **Custom Commands**: Creating shell scripts to extend functionality  
- **PATH Manipulation**: Adding directories to PATH to make commands accessible  
- **Built-in vs External Commands**: Understanding which commands rely on PATH  

### Steps to Get the Flag
1. **Create a directory for your custom commands**:  
   ```bash
   mkdir /home/hacker/mycommands
   ```

2. **Create the `win` script** using one of these methods:

   **Method 1: Use absolute path to `cat`**  
   ```bash
   echo '#!/bin/bash' > /home/hacker/mycommands/win
   echo '/bin/cat /flag' >> /home/hacker/mycommands/win
   ```

   **Method 2: Use `read` builtin (no PATH dependency)**  
   ```bash
   echo '#!/bin/bash' > /home/hacker/mycommands/win
   echo 'read flag < /flag && echo $flag' >> /home/hacker/mycommands/win
   ```

   **Method 3: Preserve PATH while adding your directory**  
   ```bash
   echo '#!/bin/bash' > /home/hacker/mycommands/win
   echo 'cat /flag' >> /home/hacker/mycommands/win
   ```

3. **Make the script executable**:  
   ```bash
   chmod +x /home/hacker/mycommands/win
   ```

4. **Run the challenge with appropriate PATH**:

   **For Methods 1 & 2** (win doesn't need external commands):  
   ```bash
   PATH=/home/hacker/mycommands /challenge/run
   ```

   **For Method 3** (win needs standard PATH for `cat`):  
   ```bash
   PATH=/home/hacker/mycommands:$PATH /challenge/run
   ```

**Note**  
- Method 1 is most reliable as it doesn't depend on PATH at all  
- Method 2 uses bash builtins, avoiding external command dependencies  
- Method 3 preserves the existing PATH while adding your directory  
- The challenge will find and execute your `win` command, which will output the flag

---

## Hijacking Commands
### Challenge Description
Create a fake `rm` command that prevents the deletion of the flag while allowing the challenge program to run successfully, then retrieve the flag.

### Concepts Learned
- **Command Interception**: Replacing system commands with custom versions  
- **PATH Manipulation**: Controlling command resolution order  
- **Scripting**: Creating executable scripts that mimic system commands  

### Steps to Get the Flag
1. **Create a directory for custom commands**:  
   ```bash
   mkdir /home/hacker/mybin
   ```

2. **Create a fake `rm` script** that preserves the flag:  
   ```bash
   cat > /home/hacker/mybin/rm << 'EOF'
   #!/bin/bash
   # Check if any arguments contain the flag file
   for arg in "$@"; do
       if [ "$arg" = "/flag" ]; then
           echo "Fake rm: preserving /flag"
           # Remove /flag from arguments
           continue
       fi
       new_args+=" $arg"
   done
   # Call real rm with modified arguments
   /bin/rm $new_args
   EOF
   ```

3. **Make the script executable**:  
   ```bash
   chmod +x /home/hacker/mybin/rm
   ```

4. **Run the challenge with custom PATH**:  
   ```bash
   PATH=/home/hacker/mybin:$PATH /challenge/run
   ```

5. **Read the preserved flag**:  
   ```bash
   cat /flag
   ```

**Alternative Simpler Approach**  
Create a fake `rm` that does nothing:  
```bash
echo '#!/bin/bash' > /home/hacker/mybin/rm
echo 'echo "Fake rm: doing nothing"' >> /home/hacker/mybin/rm
chmod +x /home/hacker/mybin/rm
PATH=/home/hacker/mybin:$PATH /challenge/run
cat /flag
```

**Note**  
- The fake `rm` intercepts the deletion attempt and prevents the flag from being removed  
- The challenge program continues execution normally  
- After the challenge completes, the flag remains accessible  
- This demonstrates how command interception can be used for security testing and system protection
