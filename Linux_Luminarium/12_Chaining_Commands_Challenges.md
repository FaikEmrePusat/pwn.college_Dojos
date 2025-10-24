# Chaining Commands
<p>In the piping module, you've explored the concept of using several commands, with data flowing between them via pipes, to accomplish something slightly more complex than the individual commands can do.
Of course, this concept also applies independent of the data transfer: sometimes, you might want to run several commands in quick succession to achieve some cumulative effect.</p>
<p>This module will cover a few ways, aside from piping, that commands can be chained.
By the end, you'll be on your way to writing <em>shell scripts</em>!</p>

---

## Chaining with Semicolons
### Challenge Description
Run `/challenge/pwn` and `/challenge/college` sequentially using the `;` operator to chain commands.

### Concepts Learned
- **Command Chaining with `;`**: Executes multiple commands sequentially, regardless of whether previous commands succeed or fail  
- **Sequential Execution**: Commands run one after another in the order specified  

### Steps to Get the Flag
1. **Run both commands chained with `;`**:  
   ```bash
   /challenge/pwn ; /challenge/college
   ```  
   This will execute `/challenge/pwn` first, then `/challenge/college` regardless of the first command's success.

2. **The second command will output the flag after the first completes**

**Note**  
- Using `;` differs from `&&` (which only runs the second command if the first succeeds)  
- Both commands will execute sequentially in the current shell session

---

## Building on Success
### Challenge Description
Run `/challenge/first-success` and `/challenge/second` using the `&&` operator to execute the second command only if the first succeeds.

### Concepts Learned
- **`&&` operator**: Executes the second command only if the first command exits successfully (exit code 0)  
- **Conditional Execution**: Useful for creating command chains where subsequent commands depend on previous success  

### Steps to Get the Flag
1. **Run the commands with `&&`**:  
   ```bash
   /challenge/first-success && /challenge/second
   ```  
   This will execute `/challenge/second` only if `/challenge/first-success` runs successfully.

2. **The second command will output the flag when the condition is met**

**Note**  
- If `/challenge/first-success` fails (non-zero exit code), `/challenge/second` won't run  
- This demonstrates how to create dependent command sequences using exit codes

---

## Handling Failure
### Challenge Description
Run `/challenge/first-failure` and `/challenge/second` using the `||` operator to execute the second command only if the first fails.

### Concepts Learned
- **`||` operator**: Executes the second command only if the first command fails (non-zero exit code)  
- **Error Handling**: Useful for providing fallback behavior when commands fail  
- **Conditional Execution**: Creates command chains where failure triggers alternative actions  

### Steps to Get the Flag
1. **Run the commands with `||`**:  
   ```bash
   /challenge/first-failure || /challenge/second
   ```  
   This will execute `/challenge/second` only if `/challenge/first-failure` fails.

2. **The second command will output the flag when the first command fails**

**Note**  
- If `/challenge/first-failure` succeeds (exit code 0), `/challenge/second` won't run  
- This demonstrates how to create fallback command sequences using exit codes

---

## Your First Shell Script
### Challenge Description
Create a shell script named `x.sh` that runs `/challenge/pwn` and `/challenge/college` sequentially, then execute the script using `bash` to get the flag.

### Concepts Learned
- **Shell Scripts**: Files containing sequences of shell commands that can be executed together  
- **Script Execution**: Running shell scripts with `bash script_name.sh`  
- **Command Sequencing**: Multiple commands in a script run in order when the script executes  

### Steps to Get the Flag
1. **Create the shell script `x.sh`**:  
   ```bash
   echo '/challenge/pwn' > x.sh
   echo '/challenge/college' >> x.sh
   ```  
   Or use a text editor to create the file with both commands.

2. **Make the script executable (optional, but good practice)**:  
   ```bash
   chmod +x x.sh
   ```  

3. **Execute the script**:  
   ```bash
   bash x.sh
   ```  
   This will run both commands sequentially and output the flag.

**Alternative - Create and run in one step**:  
```bash
echo -e '/challenge/pwn\n/challenge/college' | bash
```

**Note**  
- The script doesn't need execute permissions when run with `bash x.sh`  
- Using a text editor (like VSCode or the Desktop Text Editor) makes script creation easier for complex tasks  
- This demonstrates how to automate command sequences using shell scripts

---

## Redirecting Script Output
To complete this challenge, you need to create a shell script that runs `/challenge/pwn` and `/challenge/college` sequentially, and then pipe the output of that script to `/challenge/solve`. Here's how to do it:

### Steps:
1. **Create a shell script** named `script.sh` with the following content:
   ```bash
   /challenge/pwn
   /challenge/college
   ```
   You can create this file using a text editor or by running the following commands in the terminal:
   ```bash
   echo '/challenge/pwn' > script.sh
   echo '/challenge/college' >> script.sh
   ```

2. **Run the script and pipe its output** to `/challenge/solve`:
   ```bash
   bash script.sh | /challenge/solve
   ```
   This will execute the script and send all output from both commands to `/challenge/solve`, which will then process it and output the flag.

### Explanation:
- The shell script runs both commands in order, and their combined output is piped to `/challenge/solve`.
- Using `bash script.sh` ensures the script is executed by the shell, and the pipe (`|`) redirects the standard output to the next command.

This method demonstrates how to chain multiple commands through a script and use piping to process their output with another program.

---

## Executable Shell Scripts
### Challenge Description
Create an executable shell script that runs `/challenge/solve` and execute it directly without explicitly calling `bash`.

### Concepts Learned
- **Executable Scripts**: Shell scripts can be made executable and run directly  
- **Shebang Line**: The `#!/bin/bash` line tells the system which interpreter to use  
- **Execution Methods**: Direct execution vs. explicit interpreter invocation  

### Steps to Get the Flag
1. **Create the shell script** (e.g., `solve.sh`) with a shebang line:  
   ```bash
   echo '#!/bin/bash' > solve.sh
   echo '/challenge/solve' >> solve.sh
   ```  
   Or use a text editor to create the file with these contents.

2. **Make the script executable**:  
   ```bash
   chmod +x solve.sh
   ```  

3. **Execute the script directly**:  
   ```bash
   ./solve.sh
   ```  
   This will run the script and output the flag.

**Note**  
- The shebang line (`#!/bin/bash`) tells the system to use bash to interpret the script  
- The script must have execute permissions (`chmod +x`) to run directly  
- This demonstrates how to create self-executing scripts without needing to explicitly call the interpreter

---

## Understanding Shebangs
### Challenge Description
Create an executable shell script at `/home/hacker/solve.sh` with a proper shebang line that outputs "hack the planet", then run `/challenge/run` to verify it works.

### Concepts Learned
- **Shebang Line**: `#!/bin/bash` must be the first line of executable scripts  
- **Script Location**: Placing the script in `/home/hacker/solve.sh`  
- **Executable Permissions**: Scripts must have execute permissions to run directly  

### Steps to Get the Flag
1. **Create the script with proper shebang**:  
   ```bash
   echo '#!/bin/bash' > /home/hacker/solve.sh
   echo 'echo "hack the planet"' >> /home/hacker/solve.sh
   ```  

2. **Make the script executable**:  
   ```bash
   chmod +x /home/hacker/solve.sh
   ```  

3. **Verify the script works**:  
   ```bash
   /home/hacker/solve.sh
   ```  
   This should output "hack the planet".

4. **Run the challenge verification**:  
   ```bash
   /challenge/run
   ```  
   The challenge will detect your properly configured script and output the flag.

**Note**  
- Ensure the shebang is exactly `#!/bin/bash` as the first line with no leading spaces  
- The script must be at the exact path `/home/hacker/solve.sh`  
- This demonstrates proper shebang usage for creating executable scripts

---

## Scripting with Arguments
### Challenge Description
Create a script at `/home/hacker/solve.sh` that takes two arguments and outputs them in reverse order, then run `/challenge/run` to get the flag.

### Concepts Learned
- **Script Arguments**: Access command-line arguments using `$1`, `$2`, etc.  
- **Argument Reversal**: Output arguments in reverse order  
- **Script Execution**: Run scripts with arguments to test functionality  

### Steps to Get the Flag
1. **Create the script with proper shebang and logic**:  
   ```bash
   echo '#!/bin/bash' > /home/hacker/solve.sh
   echo 'echo "$2 $1"' >> /home/hacker/solve.sh
   ```  

2. **Make the script executable**:  
   ```bash
   chmod +x /home/hacker/solve.sh
   ```  

3. **Test the script**:  
   ```bash
   /home/hacker/solve.sh pwn college
   ```  
   This should output: `college pwn`

4. **Run the challenge verification**:  
   ```bash
   /challenge/run
   ```  
   The challenge will test your script and output the flag.

**Note**  
- The script must be at the exact path `/home/hacker/solve.sh`  
- Ensure the shebang is the first line with no leading spaces  
- The script should handle exactly two arguments and output them in reverse order

---

## Scripting with Conditionals
### Challenge Description
Create a script at `/home/hacker/solve.sh` that takes one argument and outputs "college" only if the argument is "pwn", then run `/challenge/run` to get the flag.

### Concepts Learned
- **Conditional Logic**: Using `if` statements in bash scripts  
- **String Comparison**: Using `==` operator within `[ ]` for string equality checks  
- **Argument Handling**: Accessing script arguments with `$1`

### Steps to Get the Flag
1. **Create the script with conditional logic**:  
   ```bash
   cat > /home/hacker/solve.sh << 'EOF'
   #!/bin/bash
   if [ "$1" == "pwn" ]
   then
       echo "college"
   fi
   EOF
   ```

2. **Make the script executable**:  
   ```bash
   chmod +x /home/hacker/solve.sh
   ```

3. **Test the script**:  
   ```bash
   /home/hacker/solve.sh pwn        # Should output "college"
   /home/hacker/solve.sh foo        # Should output nothing
   ```

4. **Run the challenge verification**:  
   ```bash
   /challenge/run
   ```  
   The challenge will test your script and output the flag.

**Note**  
- The script must be at the exact path `/home/hacker/solve.sh`  
- Ensure proper spacing in the condition: `[ "$1" == "pwn" ]`  
- The `then` and `fi` must be on separate lines (or separated by semicolons)  
- This demonstrates basic conditional logic in bash scripting

---

## Scripting with Default Cases
### Challenge Description
Create a script at `/home/hacker/solve.sh` that takes one argument and outputs "college" if the argument is "pwn", otherwise outputs "nope". Then run `/challenge/run` to get the flag.

### Concepts Learned
- **If-Else Logic**: Using `else` clause to handle cases where the condition is false  
- **String Comparison**: Checking argument value with `[ "$1" == "pwn" ]`  
- **Conditional Output**: Different outputs based on the input argument  

### Steps to Get the Flag
1. **Create the script with if-else logic**:  
   ```bash
   cat > /home/hacker/solve.sh << 'EOF'
   #!/bin/bash
   if [ "$1" == "pwn" ]
   then
       echo "college"
   else
       echo "nope"
   fi
   EOF
   ```

2. **Make the script executable**:  
   ```bash
   chmod +x /home/hacker/solve.sh
   ```

3. **Test the script**:  
   ```bash
   /home/hacker/solve.sh pwn        # Should output "college"
   /home/hacker/solve.sh hack       # Should output "nope"
   /home/hacker/solve.sh anything   # Should output "nope"
   ```

4. **Run the challenge verification**:  
   ```bash
   /challenge/run
   ```  
   The challenge will test your script and output the flag.

**Note**  
- The script must be at the exact path `/home/hacker/solve.sh`  
- Ensure proper spacing in the condition: `[ "$1" == "pwn" ]`  
- The `else` clause handles all cases where the condition is false  
- This demonstrates basic if-else logic in bash scripting

---

## Scripting with Multiple Conditions
### Challenge Description
Create a script at `/home/hacker/solve.sh` that uses multiple `elif` conditions to handle different input arguments with specific outputs, then run `/challenge/run` to get the flag.

### Concepts Learned
- **Multiple Conditions**: Using `elif` to check multiple conditions in sequence  
- **String Comparison**: Checking argument values with `[ "$1" == "value" ]`  
- **Conditional Logic Flow**: Only one branch executes (the first matching condition)  

### Steps to Get the Flag
1. **Create the script with multiple conditions**:  
   ```bash
   cat > /home/hacker/solve.sh << 'EOF'
   #!/bin/bash
   if [ "$1" == "hack" ]
   then
       echo "the planet"
   elif [ "$1" == "pwn" ]
   then
       echo "college"
   elif [ "$1" == "learn" ]
   then
       echo "linux"
   else
       echo "unknown"
   fi
   EOF
   ```

2. **Make the script executable**:  
   ```bash
   chmod +x /home/hacker/solve.sh
   ```

3. **Test the script**:  
   ```bash
   /home/hacker/solve.sh hack    # Should output "the planet"
   /home/hacker/solve.sh pwn     # Should output "college" 
   /home/hacker/solve.sh learn   # Should output "linux"
   /home/hacker/solve.sh foo     # Should output "unknown"
   ```

4. **Run the challenge verification**:  
   ```bash
   /challenge/run
   ```  
   The challenge will test your script and output the flag.

**Note**  
- The script must be at the exact path `/home/hacker/solve.sh`  
- Ensure proper spacing in all conditions: `[ "$1" == "value" ]`  
- Conditions are checked in order, and only the first matching one executes  
- This demonstrates complex conditional logic with multiple branches in bash scripting

---

## Reading Shell Scripts
To complete this challenge, you need to read the shell script `/challenge/run` to find the hardcoded password, then use that password when running the script to get the flag.

### Steps:
1. **Read the script using `cat`**:
   ```bash
   cat /challenge/run
   ```
   This will display the script's contents. Look for a line that sets or checks a password. For example, it might contain something like:
   ```bash
   if [ "$1" == "secretpassword" ]; then
       echo "Flag: pwn.college{...}"
   fi
   ```
   Note the password from the script.

2. **Run the script with the password as an argument**:
   ```bash
   /challenge/run [password]
   ```
   Replace `[password]` with the actual password you found.

3. **The script will output the flag**.

### Example:
If the script contains:
```bash
#!/bin/bash
if [ "$1" == "hacktheplanet" ]; then
    echo "pwn.college{example_flag}"
else
    echo "Wrong password!"
fi
```
Then you would run:
```bash
/challenge/run hacktheplanet
```
And get the flag.

This demonstrates how reading source code can reveal secrets like passwords, which is a common technique in security challenges.
