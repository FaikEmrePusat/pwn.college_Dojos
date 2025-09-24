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

## An Epic Filesystem Quest

## making directories

## finding files

## Symbolic Links

## linking files
