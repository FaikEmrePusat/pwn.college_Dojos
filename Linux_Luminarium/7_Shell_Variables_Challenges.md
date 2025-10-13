# Table of Contents

- [Shell Variables](#shell-variables)
  - [Printing Variables](#printing-variables)
  - [Setting Variables](#setting-variables)
  - [Multi-word Variables](#multi-word-variables)
  - [Exporting Variables](#exporting-variables)
  - [Printing Exported Variables](#printing-exported-variables)
  - [Storing Command Output](#storing-command-output)
  - [Reading Input](#reading-input)
  - [Reading Files](#reading-files)

# Shell Variables

<p>The Linux command line interface is actually a sophisticated programming language with which you can write actual programs!
Because the command line interface is colloquially referred to as a "shell", programs written in this language are referred to as "shell scripts".
When you're using the command line, you are basically writing a shell script line by line!</p>
<p>Like most programming languages, the shell supports variables.
This module will get you familiar with setting, printing, and using these variables!</p>

---

## Printing Variables
### Challenge Description
Print the value of the `FLAG` environment variable using `echo` to retrieve the flag.

### Concepts Learned
- **Environment Variables**: Stored values that can be accessed by the shell and programs  
- **Variable Expansion**: Using `$VARIABLE_NAME` to access variable values  
- **echo Command**: Prints arguments to standard output  

### Steps to Get the Flag
1. Run the following command to display the flag:  
   ```bash
   echo $FLAG
   ```  
   This will expand the `FLAG` variable and print its value, which is the flag for this challenge.

---

## Setting Variables
### Challenge Description
Set the `PWN` environment variable to the value `COLLEGE` and verify the assignment.

### Concepts Learned
- **Variable Assignment**: Use `VARIABLE=value` syntax (no spaces around `=`)  
- **Case Sensitivity**: Variable names and values are case-sensitive  
- **Environment Variables**: Variables can be set for the current shell session  

### Steps to Get the Flag
1. Set the `PWN` variable to `COLLEGE`:  
   ```bash
   PWN=COLLEGE
   ```  
   Note: No spaces around the `=` and both variable name and value use correct casing.

2. Verify the assignment by printing the variable:  
   ```bash
   echo $PWN
   ```  
   This should output `COLLEGE`.

3. The challenge will detect the correctly set variable and provide the flag.

**Note**  
- Use `export PWN=COLLEGE` if the variable needs to be available to child processes  
- Variable assignments are specific to the current shell session unless persisted in configuration files

---

## Multi-word Variables
### Challenge Description
Set the `PWN` environment variable to the value `COLLEGE YEAH` using proper quoting to handle the space in the value.

### Concepts Learned
- **Quoting Variables**: Use quotes (`" "` or `' '`) when variable values contain spaces  
- **Space Handling**: Without quotes, spaces separate command arguments  
- **Variable Assignment Syntax**: `VARIABLE="value with spaces"`  

### Steps to Get the Flag
1. Set the `PWN` variable using double quotes:  
   ```bash
   PWN="COLLEGE YEAH"
   ```  
   This ensures the entire string `COLLEGE YEAH` is treated as a single value.

2. Verify the assignment by printing the variable:  
   ```bash
   echo $PWN
   ```  
   This should output `COLLEGE YEAH`.

3. The challenge will detect the correctly set variable and provide the flag.

**Note**  
- Both single quotes (`' '`) and double quotes (`" "`) work for this purpose  
- The quotes are not part of the variable value - they're just syntax for the shell

---

## Exporting Variables
### Challenge Description
Set the `PWN` variable to `COLLEGE` and export it, while setting the `COLLEGE` variable to `PWN` without exporting it. Then, run `/challenge/run` to receive the flag.

### Concepts Learned
- **Exporting Variables**: Using `export` makes variables available to child processes.  
- **Non-exported Variables**: Variables set without `export` are local to the current shell and not passed to child processes.  
- **Variable Assignment**: Remember to use no spaces around the `=` sign.  

### Steps to Get the Flag
1. Set and export the `PWN` variable:  
   ```bash
   export PWN=COLLEGE
   ```  
2. Set the `COLLEGE` variable without exporting:  
   ```bash
   COLLEGE=PWN
   ```  
3. Run the challenge program:  
   ```bash
   /challenge/run
   ```  
   The program will detect the exported `PWN` variable and the non-exported `COLLEGE` variable, then output the flag.

**Note**  
Ensure you use the exact casing for variable names and values as specified. The commands must be executed in the same shell session for the variables to be set correctly.

---

## Printing Exported Variables
### Challenge Description
Use the `env` command to display all exported environment variables and locate the `FLAG` variable to retrieve the flag.

### Concepts Learned
- **`env` command**: Prints all exported environment variables in the current shell session.  
- **Environment Variables**: Variables that are exported and available to child processes.  

### Steps to Get the Flag
1. Run the `env` command and search for the `FLAG` variable:  
   ```bash
   env | grep FLAG
   ```  
   This will output the `FLAG` variable and its value, which is the flag for this challenge.

2. Alternatively, you can run `env` without `grep` and manually scan the output for `FLAG=`.  

This demonstrates how to inspect environment variables using `env`.

---

## Storing Command Output
### Challenge Description
Use command substitution to store the output of `/challenge/run` in a variable called `PWN`, then display the variable to retrieve the flag.

### Concepts Learned
- **Command Substitution**: Using `$(command)` to capture command output and assign it to a variable  
- **Variable Assignment**: Storing command output in a variable for later use  

### Steps to Get the Flag
1. Capture the output of `/challenge/run` into the `PWN` variable:  
   ```bash
   PWN=$(/challenge/run)
   ```  
2. Display the contents of the `PWN` variable to see the flag:  
   ```bash
   echo "$PWN"
   ```  

This demonstrates how to capture and reuse command output using command substitution.

---
  
## Reading Input
### Challenge Description
Use the `read` command to set the `PWN` variable to the value "COLLEGE" by providing it as user input.

### Concepts Learned
- **`read` command**: Reads input from standard input and stores it in a variable  
- **Interactive input**: The command waits for user input before continuing  

### Steps to Get the Flag
1. Run the `read` command with the `PWN` variable:  
   ```bash
   read PWN
   ```  
2. When prompted for input, type:  
   ```
   COLLEGE
   ```  
   Then press **Enter**.

3. Verify the variable was set correctly:  
   ```bash
   echo $PWN
   ```  
   This should output `COLLEGE`.

4. The challenge will detect the correctly set variable and provide the flag.

**Note**  
- You can also use `read -p "Enter value: " PWN` to provide a custom prompt  
- The variable is set in the current shell session after you provide the input

---

## Reading Files
### Challenge Description
Use input redirection with the `read` command to set the `PWN` variable with the contents of the `/challenge/read_me` file.

### Concepts Learned
- **Input Redirection**: Using `<` to redirect file contents to a command's standard input  
- **Reading Files with `read`**: The `read` command can read from redirected input instead of user input  
- **Dynamic File Content**: The file content changes, so the command must read it directly  

### Steps to Get the Flag
1. Read the file contents into the `PWN` variable using input redirection:  
   ```bash
   read PWN < /challenge/read_me
   ```  
   This reads the first line of the file into the variable.

2. Verify the variable was set correctly:  
   ```bash
   echo $PWN
   ```  
   This will display the current contents of `/challenge/read_me`.

3. The challenge will detect the correctly set variable and provide the flag.

**Note**  
- This method only reads the first line of the file  
- For multi-line files, different approaches would be needed  
- The command executes quickly, handling the changing file content dynamically
