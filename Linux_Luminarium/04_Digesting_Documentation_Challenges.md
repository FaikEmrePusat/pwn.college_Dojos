# Table of Contents

- [Digesting Documentation](#digesting-documentation)
  - [Learning From Documentation](#learning-from-documentation)
  - [Learning Complex Usage](#learning-complex-usage)
  - [Reading Manuals](#reading-manuals)
  - [Searching Manuals](#searching-manuals)
  - [Searching For Manuals](#searching-for-manuals)
  - [Helpful Programs](#helpful-programs)
  - [Help for Builtins](#help-for-builtins)

---

# Digesting Documentation
<p>This module will teach you one of the most important Linux skills: looking for help on how to use programs.
This skill will serve you quite well in your journey.
Dive in below!</p>

---

## Learning From Documentation
### Challenge Description
Execute `/challenge/challenge` with the `--giveflag` argument to retrieve the flag.

### Concepts Learned
- **Command-line arguments**: Programs often require specific arguments to function correctly.  
- **Documentation**: Understanding program usage through provided documentation is essential.  

### Steps to Get the Flag
1. Run the following command in the terminal:  
   ```bash
   /challenge/challenge --giveflag
   ```  
2. The program will output the flag.  

This demonstrates the importance of reading documentation and using the correct arguments when invoking programs.

---

## Learning Complex Usage
### Challenge Description
Execute `/challenge/challenge` with the `--printfile` argument followed by the path to the flag file to retrieve the flag.

### Concepts Learned
- **Nested arguments**: Some commands require arguments that themselves take additional arguments.  
- **Flag location**: The flag is typically located at `/flag`.  

### Steps to Get the Flag
1. Run the following command in the terminal:  
   ```bash
   /challenge/challenge --printfile /flag
   ```  
2. The program will read and output the contents of the flag file.  

This demonstrates how to handle commands with complex argument structures, where an argument requires its own parameter.

---

## Reading Manuals
### Challenge Description
Use the `man` command to find the secret option for `/challenge/challenge` that will print the flag, then execute the program with that option.

### Concepts Learned
- **`man` command**: Displays manual pages for commands, providing documentation on usage and options.  
- **Secret option**: The manual page for `challenge` contains a hidden or specific option that triggers the flag output.  

### Steps to Get the Flag
1. View the manual page for `challenge` to find the secret option:  
   ```bash
   man challenge
   ```  
   - Use arrow keys or PgUp/PgDn to scroll through the manual.  
   - Look for options in the SYNOPSIS or DESCRIPTION sections that might print the flag (e.g., options like `--flag`, `--secret`, or similar).  
   - Press `q` to quit the manual after reading.  

2. Execute `/challenge/challenge` with the discovered option. For example, if the option is `--giveflag`:  
   ```bash
   /challenge/challenge --giveflag
   ```  
   Replace `--giveflag` with the actual option found in the manual.  

3. The program will output the flag.  

This demonstrates how to use the `man` command to access documentation and discover command-line options for programs.

---

## Searching Manuals
### Challenge Description
Use the `man` command to find the secret option in the challenge's manual page that will output the flag, then execute the program with that option.

### Concepts Learned
- **`man` command**: Displays manual pages with detailed documentation
- **Searching in man pages**: Use `/` to search forward, `?` to search backward
- **Navigation**: Use `n` for next match, `N` for previous match

### Steps to Get the Flag
1. Open the manual page for the challenge:
   ```bash
   man challenge
   ```
2. Search for flag-related options by typing `/flag` and pressing Enter
3. Navigate through results with `n` (next) and `N` (previous)
4. Look for an option that mentions printing or displaying the flag
5. Once found, note the option name and quit the manual with `q`
6. Execute the challenge with the discovered option:
   ```bash
   /challenge/challenge --option-name
   ```
   Replace `--option-name` with the actual option found in the manual

This teaches manual page navigation and searching skills essential for discovering program functionality.

---

## Searching For Manuals
### Challenge Description
Find the randomly named manpage for the `/challenge/challenge` program using the man command's search functionality, then use the information from that manpage to execute `/challenge/challenge` with the correct option to retrieve the flag.

### Concepts Learned
- **`man` command**: Used to display manual pages. The `-k` option searches the manpage database for keywords.  
- **Manpage search**: Since the manpage name is randomized, searching by keyword (e.g., "challenge") is necessary to find the relevant documentation.  
- **Secret option**: The manpage will contain an option that, when used with `/challenge/challenge`, outputs the flag.  

### Steps to Get the Flag
1. Read the `man` manual to understand how to search:  
   ```bash
   man man
   ```  
   Look for search options like `-k` or `--search` in the description.  

2. Search the manpage database for entries related to "challenge":  
   ```bash
   man -k challenge
   ```  
   This will list manpages with "challenge" in their name or description. Note the random name of the manpage for the challenge program.  

3. Open the identified manpage using its random name:  
   ```bash
   man <random-name>
   ```  
   Replace `<random-name>` with the name found in step 2.  

4. Within the manpage, search for an option that prints the flag. Use `/` to search for keywords like "flag" or "print". Navigate with `n` and `N`.  

5. Once the option is found (e.g., `--giveflag`), quit the manpage with `q` and run `/challenge/challenge` with that option:  
   ```bash
   /challenge/challenge --giveflag
   ```  
   Replace `--giveflag` with the actual option from the manpage.  

6. The program will output the flag.  

This challenge teaches how to search and navigate manpages effectively to discover program usage.

---

## Helpful Programs
### Challenge Description
Use the `--help` option with `/challenge/challenge` to discover how to retrieve the flag.

### Concepts Learned
- **Help options**: Many programs provide usage information when invoked with `--help`, `-h`, or similar arguments.  
- **Self-documentation**: Programs can output their own documentation when given specific arguments, eliminating the need for external man pages.  

### Steps to Get the Flag
1. Run the following command to view the help message:  
   ```bash
   /challenge/challenge --help
   ```  
2. From the help output, identify the option that prints the flag (e.g., `--giveflag` or similar).  
3. Execute the program with the identified option:  
   ```bash
   /challenge/challenge --giveflag
   ```  
   Replace `--giveflag` with the actual option found in the help message.  

This will output the flag. This challenge demonstrates how to access built-in help for programs without relying on external documentation.

---

## Help for Builtins
### Challenge Description
Use the `help` command to find documentation for the shell builtin `challenge` and discover the secret value needed to retrieve the flag.

### Concepts Learned
- **Shell builtins**: Commands implemented directly within the shell rather than as separate programs
- **Builtin documentation**: Use `help` instead of `man` for shell builtins
- **Secret argument**: The builtin requires a specific argument to output the flag

### Steps to Get the Flag
1. Get help for the challenge builtin:
   ```bash
   help challenge
   ```
2. Read the documentation to identify the required argument format
3. Execute the builtin with the discovered argument:
   ```bash
   challenge [secret_argument]
   ```
   Replace `[secret_argument]` with the actual value from the help documentation

This teaches how to access documentation for shell builtins using the `help` command.
