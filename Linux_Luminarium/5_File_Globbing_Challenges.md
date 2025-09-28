# File Globbing
<p>Even just a few levels in, you might already be tired of typing out all these file paths.
Luckily, the shell has a solution: globbing!
That's what we'll learn in this module.</p>
<p>Before executing commands that you enter, the shell first performs <em>expansions</em> on them, and one of these expansions is globbing.
Globbing lets you reference files without typing them all out, or typing out their full paths.
Let's dig in!</p>

---

## Matching with *
### Challenge Description
Change directory to `/challenge` using a glob pattern of at most four characters in the `cd` command, then execute `/challenge/run` to get the flag.

### Concepts Learned
- **Globbing**: Using wildcard characters like `*` to match file or directory names. The `*` matches any sequence of characters except `/` or leading `.`.  
- **Absolute Path Globbing**: Patterns starting with `/` are resolved from the root directory.  
- **Directory Change**: The `cd` command changes the current working directory based on the expanded glob pattern.  

### Steps to Get the Flag
1. From your home directory (`/home/hacker`), use `cd` with a glob pattern that matches `/challenge` but has at most four characters:  
   ```bash
   cd /c*
   ```  
   This pattern (`/c*`) is three characters long and should expand to `/challenge` if it is the only directory in root starting with `c`.  
2. Verify that you are in `/challenge` by checking the prompt or using `pwd`.  
3. Run the challenge program to get the flag:  
   ```bash
   /challenge/run
   ```  

This demonstrates how globbing can be used to shorten paths when navigating the filesystem.

---

## Matching with ?
### Challenge Description
Change directory to `/challenge` using a glob pattern that replaces the letters 'c' and 'l' with the `?` wildcard, then execute `/challenge/run` to get the flag.

### Concepts Learned
- **`?` wildcard**: Matches any single character in a filename or path.  
- **Globbing in paths**: Using wildcards to construct paths without specifying exact letters.  
- **Absolute path with wildcards**: The pattern must uniquely match `/challenge` by replacing 'c' and 'l' with `?`.  

### Steps to Get the Flag
1. From your home directory (`/home/hacker`), use `cd` with a pattern that replaces 'c' and 'l' in "challenge" with `?`:  
   ```bash
   cd /?ha??enge
   ```  
   This pattern matches `/challenge` because `?` matches 'c' for the first character, and `?` matches each 'l' in the fourth and fifth positions.  
2. Verify that you are in `/challenge` by checking the prompt (e.g., `hacker@dojo:/challenge$`).  
3. Run the challenge program to get the flag:  
   ```bash
   /challenge/run
   ```  
   Alternatively, since you are in the `/challenge` directory, you can use:  
   ```bash
   ./run
   ```  

This demonstrates the use of the `?` wildcard for precise single-character matching in paths.

---

## Matching with []
### Challenge Description
Use bracket globbing to pass multiple files as arguments to `/challenge/run` by specifying a single glob pattern that matches `file_a`, `file_b`, `file_s`, and `file_h` in the `/challenge/files` directory.

### Concepts Learned
- **Bracket Globbing**: Using `[]` to match a subset of characters. For example, `[absh]` matches any one of the characters 'a', 'b', 's', or 'h'.  
- **Glob Expansion**: The shell expands the glob pattern into multiple arguments when passed to a command.  
- **Relative Paths**: The glob pattern is resolved relative to the current working directory.  

### Steps to Get the Flag
1. Change to the `/challenge/files` directory:  
   ```bash
   cd /challenge/files
   ```  
2. Run `/challenge/run` with the bracket glob pattern:  
   ```bash
   /challenge/run file_[absh]
   ```  
   This pattern expands to `file_a file_b file_s file_h` (if all files exist), passing them as arguments to the program.  
3. The program will process the files and output the flag.  

This demonstrates how bracket globbing can efficiently match multiple files with a single pattern.

---

## Matching paths with []
### Challenge Description
Run `/challenge/run` from your home directory with a single glob pattern argument that expands to the absolute paths of `file_a`, `file_b`, `file_s`, and `file_h` in `/challenge/files`.

### Concepts Learned
- **Bracket Globbing**: Using `[absh]` to match any one of the characters 'a', 'b', 's', or 'h' in the filename.  
- **Absolute Paths**: The glob pattern must include the full path from root (`/`).  
- **Shell Expansion**: The shell expands the glob pattern into multiple arguments before passing them to the program.  

### Steps to Get the Flag  
1. From your home directory (`/home/hacker`), run the following command:  
   ```bash
   /challenge/run /challenge/files/file_[absh]
   ```  
   This pattern expands to the absolute paths `/challenge/files/file_a`, `/challenge/files/file_b`, `/challenge/files/file_s`, and `/challenge/files/file_h`.  
2. The program will process these files and output the flag.  

This demonstrates how bracket globbing can be used with absolute paths to match multiple files efficiently.

---

## Multiple globs
### Challenge Description 
Change to the `/challenge/files` directory and run `/challenge/run` with a single glob pattern argument that matches all files containing the letter 'p'. The pattern must be three characters or less and contain two `*` wildcards.

### Concepts Learned
- **Globbing with Multiple Wildcards**: Using `*` to match any sequence of characters, and combining them with literal characters to form patterns.  
- **Pattern Efficiency**: The pattern `*p*` matches any filename that contains the letter 'p' anywhere in the name.  
- **Shell Expansion**: The shell expands the glob pattern into multiple filenames before passing them to the program.  

### Steps to Get the Flag  
1. Change to the `/challenge/files` directory:  
   ```bash
   cd /challenge/files
   ```  
2. Run `/challenge/run` with the glob pattern `*p*`:  
   ```bash
   /challenge/run *p*
   ```  
   This pattern is three characters long and expands to all files in the current directory that contain the letter 'p'.  
3. The program will process the matched files and output the flag.  

This demonstrates how to use multiple wildcards in a single glob pattern to match files based on content within their names.

---

## Mixing globs
### Challenge Description
Change to the `/challenge/files` directory and run `/challenge/run` with a single glob pattern argument that matches the files "challenging", "educational", and "pwning". The pattern must be six characters or less.

### Concepts Learned
- **Globbing with Multiple Wildcards**: Using `*` to match any sequence of characters, combined with literal characters to form a pattern that matches specific files.  
- **Pattern Efficiency**: The pattern `*i*n*` matches any filename that contains the letter 'i' followed by the letter 'n' anywhere in the name, which applies to all three target files.  
- **Shell Expansion**: The shell expands the glob pattern into multiple filenames before passing them to the program.  

### Steps to Get the Flag  
1. Change to the `/challenge/files` directory:  
   ```bash
   cd /challenge/files
   ```  
2. Run `/challenge/run` with the glob pattern `*i*n*`:  
   ```bash
   /challenge/run *i*n*
   ```  
   This pattern is four characters long and expands to include "challenging", "educational", and "pwning" (assuming no other files in the directory contain 'i' followed by 'n').  
3. The program will process the matched files and output the flag.  

This demonstrates how to use a concise glob pattern with multiple wildcards to match multiple files based on common character sequences.

---

## Exclusionary globbing
### Challenge Description
Change to the `/challenge/files` directory and run `/challenge/run` with a single glob pattern argument that matches all files NOT starting with the letters 'p', 'w', or 'n'.

### Concepts Learned  
- **Negative Bracket Globbing**: Using `[^...]` or `[!...]` to match characters NOT in the specified set.  
- **Pattern Structure**: The pattern should exclude files starting with 'p', 'w', or 'n'.  
- **Shell Expansion**: The shell expands the negative glob pattern to include all files that don't match the excluded characters.  

### Steps to Get the Flag  
1. Change to the `/challenge/files` directory:  
   ```bash
   cd /challenge/files
   ```  
2. Run `/challenge/run` with the negative glob pattern `[^pwn]*`:  
   ```bash
   /challenge/run [^pwn]*
   ```  
   This pattern matches all files that do NOT start with 'p', 'w', or 'n'.  
3. The program will process the matched files and output the flag.  

**Note**  
- `[^pwn]` matches any single character except 'p', 'w', or 'n'  
- The `*` wildcard then matches the rest of the filename  
- This pattern effectively excludes files starting with the specified letters while including all others

---

## Tab completion
### Challenge Description
Use tab completion to read the `/challenge/pwncollege` file, as manual typing of the full filename is prevented.

### Concepts Learned  
- **Tab Completion**: Pressing the Tab key in the shell automatically completes partially typed commands or filenames.  
- **Filename Trickery**: The challenge prevents manual typing of the full filename, requiring tab completion.  

### Steps to Get the Flag  
1. Start typing the command to read the file:  
   ```bash
   cat /challenge/pwn
   ```  
2. Press the **Tab** key to auto-complete the filename to `pwncollege`.  
3. The command will become:  
   ```bash
   cat /challenge/pwncollege
   ```  
4. Press **Enter** to execute the command and display the flag.  

**Note**  
- Tab completion helps avoid typing errors and is essential when exact filenames are difficult to type manually.  
- The shell will only auto-complete if the partial filename is unique in the directory.

---

## Multiple options for tab completion
### Challenge Description
Use tab completion to navigate and read the correct file in `/challenge/files` that starts with `pwncollege` and contains the flag.

### Concepts Learned  
- **Tab Completion**: Pressing the Tab key in the shell automatically completes partially typed commands or filenames. If there are multiple matches, pressing Tab twice displays all options, allowing you to cycle through or refine your input.  
- **Multiple Files**: The directory contains several files starting with `pwncollege`, so tab completion helps find the exact filename without typing it fully.  

### Steps to Get the Flag  
1. Start from your home directory and use tab completion with the full path for efficiency:  
   ```bash
   cat /challenge/files/p
   ```  
   Press **Tab** once. If multiple files start with `p`, the shell may complete to the common prefix (e.g., `pwncollege`) or show a list.  
   - If it completes to `pwncollege`, press **Tab** again to see all files starting with `pwncollege` (e.g., `pwncollege_flag`, `pwncollege_data`, etc.).  
   - If it doesn't complete, press **Tab** twice to view all options, then type more characters to narrow down (e.g., `pwncollege_f` and press **Tab**).  

2. Once the correct filename is displayed (e.g., `/challenge/files/pwncollege_flag`), press **Enter** to execute the command and display the flag.  

**Example Interaction**  
```bash
hacker@dojo:~$ cat /challenge/files/p
# Press Tab once, might complete to pwncollege
hacker@dojo:~$ cat /challenge/files/pwncollege
# Press Tab twice to see options: pwncollege_flag  pwncollege_other
hacker@dojo:~$ cat /challenge/files/pwncollege_flag
# Press Enter to get the flag
pwn.college{flag_here}
```

This demonstrates how tab completion simplifies navigating directories with multiple similar filenames, ensuring accuracy and efficiency.

---

## Tab completion on commands
### Challenge Description
Use tab completion to run a command starting with "pwncollege" that outputs the flag.

### Concepts Learned  
- **Tab Completion for Commands**: The shell can auto-complete command names, similar to filenames, by pressing the Tab key. This helps execute commands quickly without typing the full name.  
- **Command Execution**: After auto-completion, running the command will perform its intended action, such as outputting the flag.  

### Steps to Get the Flag  
1. In the terminal, type `pwncollege` but do not press Enter.  
2. Press the **Tab** key to auto-complete the command. If multiple commands start with "pwncollege", press Tab twice to see options and type more characters to narrow down.  
3. Once the command is completed (e.g., `pwncollege_command`), press **Enter** to execute it.  
4. The command will run and output the flag.  

**Note**  
- Ensure the command is in your PATH; the pwn.college environment should be set up correctly for this.  
- Use tab completion carefully to avoid accidentally running wrong commands.
