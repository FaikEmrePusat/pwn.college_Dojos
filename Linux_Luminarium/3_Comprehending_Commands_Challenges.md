# Comprehending Commands
<p>This module will expose you to some useful Linux commands that will serve you well for the rest of your journey here!
It is FAR from an exhaustive list, and we'll continue to expand this module, but this should be enough to get you started.</p>
<p>So, without further ado, let's learn some commands!</p>

## cat: not the pet, but the command!
### Challenge Description   
Read the `flag` file in your home directory using the `cat` command.

### Concepts Learned 
- **`cat` command**: Used to read and concatenate files.  
- **Home directory**: Your shell starts in `/home/hacker`, where the `flag` file is located.  

### Steps to Get the Flag
1. From your home directory (prompt: `hacker@dojo:~$`), run:  
   ```bash
   cat flag
   ```  
2. The contents of the `flag` file will be displayed, showing the flag.  

This demonstrates basic file reading with `cat` from the current directory.

---

## catting absolute paths
### Challenge Description 
Read the flag using `cat` with its absolute path `/flag`.

### Concepts Learned 
- **Absolute Path**: Access files directly from root (`/`) without relying on the current directory.  
- **`cat` command**: Reads file contents when provided with a path.  

### Steps to Get the Flag  
1. Run the command:  
   ```bash
   cat /flag
   ```  
2. The contents of the flag will be displayed.  

**Note**  
In pwn.college, the flag is always located at `/flag`, though it is not always directly accessible in other challenges.

---

## more catting practice
### Challenge Description
Read the flag using `cat` with its absolute path without changing directories.

### Concepts Learned 
- **Absolute Path**: Directly specify the full path to the file from root (`/`).  
- **Restriction**: The `cd` command is not allowed; you must use the full path directly.  

### Steps to Get the Flag
1. Use `cat` with the absolute path provided for the flag (e.g., `/unusual/directory/structure/flag`):  
   ```bash
   cat /absolute/path/to/flag
   ```  
2. The flag will be displayed directly in the terminal.  

**Note**  
The exact path will be unique to this challenge—replace `/absolute/path/to/flag` with the actual path given in the challenge description.

---

## grepping for a needle in a haystack
### Challenge Description
Use `grep` to search for the flag in the large file `/challenge/data.txt` by matching the flag's starting text.

### Concepts Learned 
- **`grep` command**: Searches for specific strings within files and outputs matching lines.  
- **Flag Identifier**: The flag always starts with `pwn.college`.  

### Steps to Get the Flag
1. Run the following command to search for the flag:  
   ```bash
   grep "pwn.college" /challenge/data.txt
   ```  
2. The line containing the flag will be displayed in the terminal.

---

## comparing files
### Challenge Description 
Use the `diff` command to compare two files and identify the real flag, which is the additional line in `/challenge/decoys_and_real.txt`.

### Concepts Learned 
- **`diff` command**: Compares two files line by line and displays differences.  
- **File Contents**: `/challenge/decoys_only.txt` contains 100 fake flags, while `/challenge/decoys_and_real.txt` contains the same 100 fake flags plus one real flag.  

### Steps to Get the Flag
1. Run the `diff` command to compare the files:  
   ```bash
   diff /challenge/decoys_only.txt /challenge/decoys_and_real.txt
   ```  
2. The output will show an added line (marked with `>`) which is the real flag. For example:  
   ```
   100a101
   > pwn.college{real_flag_here}
   ```  
   This indicates that after line 100 of the first file, line 101 is added in the second file, containing the real flag.  

This demonstrates how `diff` can be used to find differences between files efficiently.

---

## listing files
### Challenge Description
Find and execute the randomly named program in the `/challenge` directory using `ls`.

### Concepts Learned
- **`ls` command**: Lists the contents of directories.  
- **Absolute Path**: Use the full path to execute the program once identified.  

### Steps to Get the Flag
1. List the files in `/challenge` to find the program:  
   ```bash
   ls /challenge
   ```  
2. Note the name of the file that appears (it will be random).  
3. Execute the program using its absolute path:  
   ```bash
   /challenge/[random_name]
   ```  
   Replace `[random_name]` with the actual name from the `ls` output.  

This will run the program and output the flag.

---

## touching files
### Challenge Description
Create two files, `/tmp/pwn` and `/tmp/college`, using the `touch` command, then execute `/challenge/run` to retrieve the flag.

### Concepts Learned 
- **`touch` command**: Creates new, empty files or updates the timestamp of existing files.  
- **Absolute Path**: Use full paths to create files in the `/tmp` directory.  

### Steps to Get the Flag 
1. Create the first file:  
   ```bash
   touch /tmp/pwn
   ```  
2. Create the second file:  
   ```bash
   touch /tmp/college
   ```  
3. Run the challenge program:  
   ```bash
   /challenge/run
   ```  
4. The program will verify the files and output the flag.  

This demonstrates basic file creation with `touch` using absolute paths.

---

## removing files
### Challenge Description
Delete the `delete_me` file from your home directory using `rm`, then run `/challenge/check` to verify and get the flag.

### Concepts Learned 
- **`rm` command**: Removes files permanently  
- **File deletion**: Practice cleaning up unwanted files  

### Steps to Get the Flag  
1. Delete the file from your home directory:  
   ```bash
   rm ~/delete_me
   ```  
2. Run the verification program:  
   ```bash
   /challenge/check
   ```  
3. The program will confirm deletion and output the flag

---

## moving files
### Challenge Description
Move the `/flag` file to `/tmp/hack-the-planet` using the `mv` command, then run `/challenge/check` to verify and receive the flag.

### Concepts Learned
- **`mv` command**: Moves or renames files and directories by specifying source and destination paths.  
- **Absolute paths**: Using full paths to ensure accurate file movement.  

### Steps to Get the Flag
1. Move the flag file to the specified location:  
   ```bash
   mv /flag /tmp/hack-the-planet
   ```  
2. Execute the check program to verify the move and obtain the flag:  
   ```bash
   /challenge/check
   ```

---

## hidden files
### Challenge Description
Find and read the hidden flag file in the root directory (/) that starts with a dot.

### Concepts Learned
- **Hidden files**: Files starting with a dot (.) are hidden by default in `ls`.  
- **`ls -a`**: The `-a` flag lists all files, including hidden ones.  

### Steps to Get the Flag
1. List all files in the root directory, including hidden ones:  
   ```bash
   ls -a /
   ```  
2. Identify the hidden file (e.g., `.flag` or similar).  
3. Read the file using `cat`:  
   ```bash
   cat //.flag
   ```  
   Replace `.flag` with the actual filename from the `ls` output.  

This will display the flag.

---

## An Epic Filesystem Quest
### Challenge Description
Find the hidden flag by following clues starting from the root directory using `ls` and `cat`.

### Concepts Learned
- **Navigation**: Use `cd` to change directories.  
- **Listing files**: Use `ls` to explore directory contents.  
- **Reading files**: Use `cat` to read clue files.  

### Steps to Get the Flag
1. Start at the root directory:  
   ```bash
   cd /
   ```  
2. List the files to find a clue file (e.g., `HINT`, `CLUE`, or similar):  
   ```bash
   ls
   ```  
3. Read the clue file to get the next direction:  
   ```bash
   cat CLUE
   ```  
   (Replace `CLUE` with the actual filename found.)  
4. Follow the clue to the next directory or file. For example, if the clue says "Go to /home/hacker", then:  
   ```bash
   cd /home/hacker
   ```  
5. Repeat steps 2-4 in the new directory until you find the flag file.  
6. Once you find the flag, read it with `cat`:  
   ```bash
   cat flag_file
   ```  

This process requires iterative exploration. The clues will guide you through the filesystem until you locate the flag.
Good luck!

---

## making directories
### Challenge Description
Create a directory named `pwn` in `/tmp` and a file named `college` inside it, then run `/challenge/run` to get the flag.

### Concepts Learned
- **`mkdir` command**: Creates new directories.  
- **`touch` command**: Creates new, empty files.  
- **Absolute paths**: Use full paths to ensure accuracy.  

### Steps to Get the Flag
1. Create the directory `/tmp/pwn`:  
   ```bash
   mkdir /tmp/pwn
   ```  
2. Create the file `college` inside the directory:  
   ```bash
   touch /tmp/pwn/college
   ```  
3. Run the challenge program to verify and receive the flag:  
   ```bash
   /challenge/run
   ```  

This demonstrates directory creation and file management using absolute paths.

---

## finding files
### Challenge Description
Find the hidden flag file named "flag" somewhere in the filesystem using the `find` command.

### Concepts Learned
- **`find` command**: Searches for files and directories based on criteria like name.  
- **Permission errors**: Some directories are inaccessible; errors can be suppressed.  
- **Multiple files**: There may be multiple "flag" files; check each one for the actual flag.

### Steps to Get the Flag
1. Search for all files named "flag" from the root directory, ignoring errors:  
   ```bash
   find / -name flag 2>/dev/null
   ```  
   This lists accessible paths.  
2. Check each found file with `cat` to find the flag:  
   ```bash
   cat /path/to/flag
   ```  
   Replace `/path/to/flag` with each path from the list.  
3. Alternatively, use `grep` to search for the flag pattern (e.g., "pwn.college") directly:  
   ```bash
   find / -name flag 2>/dev/null -exec grep "pwn.college" {} \;
   ```  
   This outputs matching lines, revealing the flag quickly.

This demonstrates file searching with `find` and content inspection with `cat` or `grep`.

---

## linking files
### Challenge Description
Use a symbolic link to trick `/challenge/catflag` into reading the flag from `/flag` instead of `/home/hacker/not-the-flag`.

### Concepts Learned
- **Symbolic links (symlinks)**: Create pointers to files using `ln -s`.  
- **File redirection**: By replacing `/home/hacker/not-the-flag` with a symlink to `/flag`, accessing the symlink will redirect to the actual flag.  

### Steps to Get the Flag
1. Remove the existing `/home/hacker/not-the-flag` file (if it exists):  
   ```bash
   rm /home/hacker/not-the-flag
   ```  
2. Create a symbolic link from `/home/hacker/not-the-flag` to `/flag`:  
   ```bash
   ln -s /flag /home/hacker/not-the-flag
   ```  
3. Run the challenge program to retrieve the flag:  
   ```bash
   /challenge/catflag
   ```  

This will cause `/challenge/catflag` to read the symlink, which points to `/flag`, thus displaying the flag.
