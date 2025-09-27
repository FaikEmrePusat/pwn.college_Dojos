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


---

## Multiple globs

## Mixing globs

## Exclusionary globbing

## Tab completion

## Multiple options for tab completion

## Tab completion on commands
