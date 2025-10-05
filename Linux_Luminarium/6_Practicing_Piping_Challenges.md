# Practicing Piping
<p>You may have observed that some commands output data onto your terminal when you run them.
So far, this has printed you many flags, but like many things, the technology goes much deeper.
The mechanisms behind the handling of input and output on the commandline contribute to the commandline's power.</p>
<p>This module will teach you about <em>input and output redirection</em>.
Simply put, every process in Linux has three initial, standard channels of communication:</p>
<ul>
<li>Standard <em>Input</em> is the channel through which the process takes input. For example, your shell uses Standard Input to read the commands that you input.</li>
<li>Standard <em>Output</em> is the channel through which processes output normal data, such as the flag when it is printed to you in previous challenges or the output of utilities such as <code>ls</code>.</li>
<li>Standard <em>Error</em> is the channel through which processes output error details. For example, if you mistype a command, the shell will output, over standard error, that this command does not exist.</li>
</ul>
<p>Because these three channels are used so frequently in Linux, they are known by shorter names: <code>stdin</code>, <code>stdout</code>, <code>stderr</code>.
This module will teach you how to redirect, chain, block, and otherwise mess with these channels.
Good luck!</p>

---

## Redirecting output
### Challenge Description
Use output redirection with `>` to write the word "PWN" to a file named "COLLEGE".

### Concepts Learned
- **Output Redirection**: The `>` operator redirects command output to a file, overwriting existing content.  
- **echo Command**: Outputs text to stdout, which can be redirected to a file.  

### Steps to Get the Flag
1. Use `echo` with output redirection to create/write to the file:  
   ```bash
   echo PWN > COLLEGE
   ```  
2. Verify the file was created and contains "PWN":  
   ```bash
   cat COLLEGE
   ```  

---

This demonstrates basic output redirection to create and populate files.

## Redirecting more output
### Challenge Description  
Redirect the standard output (stdout) of `/challenge/run` to the file `myflag` to capture the flag, while allowing standard error (stderr) to display in the terminal.

### Concepts Learned
- **Output Redirection**: The `>` operator redirects stdout to a file, overwriting any existing content.  
- **Standard Error vs. Standard Output**: The program outputs the flag to stdout and diagnostic messages to stderr, so redirecting stdout alone captures only the flag.  

### Steps to Get the Flag
1. Execute the command with output redirection:  
   ```bash
   /challenge/run > myflag
   ```  
   This will write the flag to `myflag` while still displaying stderr messages in the terminal.  
2. Read the flag from the file:  
   ```bash
   cat myflag
   ```  

This demonstrates how to selectively capture command output using redirection.

---

## Appending output
### Challenge Description  
Run `/challenge/run` with append-mode output redirection to capture both halves of the flag in `/home/hacker/the-flag`.

### Concepts Learned
- **Append-Mode Redirection**: Using `>>` instead of `>` appends output to a file without overwriting existing content.  
- **Standard Output Capture**: The program writes the first half of the flag directly to the file and the second half to stdout, which must be redirected to the same file to capture the complete flag.  

### Steps to Get the Flag
1. Execute the command with append-mode redirection:  
   ```bash
   /challenge/run >> /home/hacker/the-flag
   ```  
   This ensures the second half of the flag (sent to stdout) is appended to the file containing the first half.  
2. Read the complete flag from the file:  
   ```bash
   cat /home/hacker/the-flag
   ```  

**Note**  
Using truncation mode (`>`) would overwrite the first half of the flag with the second half, making it incomplete. Append mode preserves both parts.

---

## Redirecting errors
### Challenge Description  
Redirect the standard output (stdout) of `/challenge/run` to `myflag` and the standard error (stderr) to `instructions` to capture the flag and instructions separately.

### Concepts Learned
- **File Descriptor Redirection**: Use `>` for stdout (FD 1) and `2>` for stderr (FD 2).  
- **Separate Output Streams**: The program outputs the flag to stdout and instructions/feedback to stderr.  

### Steps to Get the Flag
1. Execute the command with both redirections:  
   ```bash
   /challenge/run > myflag 2> instructions
   ```  
   This redirects stdout to `myflag` and stderr to `instructions`, so nothing appears in the terminal.  
2. Read the flag from `myflag`:  
   ```bash
   cat myflag
   ```  
3. (Optional) View the instructions from `instructions`:  
   ```bash
   cat instructions
   ```  

This demonstrates how to manage multiple output streams using file descriptor redirection.

---
## Redirecting input
To complete this challenge, you need to create a file named "PWN" containing the word "COLLEGE" and then redirect this file as input to `/challenge/run`. Here's how to do it:

### Steps:
1. Create the "PWN" file with the content "COLLEGE" using output redirection:
   ```bash
   echo COLLEGE > PWN
   ```
2. Run `/challenge/run` with input redirection from the "PWN" file:
   ```bash
   /challenge/run < PWN
   ```
3. The program will read "COLLEGE" from the file and output the flag.

### Explanation:
- The `echo COLLEGE > PWN` command writes "COLLEGE" to the file "PWN", creating it if it doesn't exist or overwriting it if it does.
- The `/challenge/run < PWN` command redirects the contents of "PWN" as standard input to the program, which processes it and returns the flag.

This demonstrates the use of both output redirection (to create a file) and input redirection (to provide input to a program).

---

## Grepping stored results
### Challenge Description  
Redirect the output of `/challenge/run` to `/tmp/data.txt` and then use `grep` to find the flag within the file.

### Concepts Learned
- **Output Redirection**: Use `>` to save command output to a file.  
- **File Search with `grep`**: Search through large files for specific patterns, such as the flag starting with "pwn.college".  

### Steps to Get the Flag
1. Redirect the output of `/challenge/run` to `/tmp/data.txt`:  
   ```bash
   /challenge/run > /tmp/data.txt
   ```  
   This creates a file with 100,000 lines, one of which contains the flag.  
2. Search for the flag using `grep` with the pattern "pwn.college":  
   ```bash
   grep "pwn.college" /tmp/data.txt
   ```  
   This will output the line containing the flag.  

This demonstrates how to combine output redirection and text searching to efficiently find information in large files.

---

## Grepping live output
### Challenge Description  
Use the pipe operator (`|`) to directly pass the output of `/challenge/run` to `grep` and search for the flag without creating an intermediate file.

### Concepts Learned
- **Pipe Operator (`|`)**: Connects the standard output of one command to the standard input of another command.  
- **Efficient Data Processing**: Avoids creating temporary files by processing data directly between commands.  

### Steps to Get the Flag
1. Run `/challenge/run` and pipe its output to `grep` to search for the flag pattern:  
   ```bash
   /challenge/run | grep "pwn.college"
   ```  
   This will output only the line containing the flag.  

This demonstrates how pipes can streamline command workflows by connecting commands directly.

---

## Grepping errors
### Challenge Description  
Redirect standard error to standard output and then pipe the combined stream to `grep` to find the flag in the error output of `/challenge/run`.

### Concepts Learned
- **File Descriptor Redirection**: Use `2>&1` to redirect stderr (FD 2) to stdout (FD 1)  
- **Combining Streams**: This allows both stdout and stderr to be processed through a pipe  
- **Pipe Operator**: `|` only handles stdout by default, so stderr must be redirected first  

### Steps to Get the Flag
1. Run `/challenge/run` with stderr redirected to stdout, then pipe to `grep`:  
   ```bash
   /challenge/run 2>&1 | grep "pwn.college"
   ```  
   This will search both stdout and stderr for the flag pattern.  

This demonstrates how to combine output streams to process error messages through standard piping operations.

---

## Filtering with grep -v
### Challenge Description  
Use `grep -v` to filter out decoy flags containing the word "DECOY" from the output of `/challenge/run` to reveal the real flag.

### Concepts Learned
- **Inverse Matching with `grep -v`**: Shows lines that do NOT match the specified pattern  
- **Filtering Noise**: Removing unwanted data to isolate the desired information  

### Steps to Get the Flag
1. Run `/challenge/run` and pipe its output to `grep -v` to exclude lines containing "DECOY":  
   ```bash
   /challenge/run | grep -v "DECOY"
   ```  
   This will display only the real flag by filtering out all decoy flags.  

This demonstrates how inverse matching can be used to clean up output by excluding unwanted patterns.

---

## Duplicating piped data with tee
### Challenge Description  
Intercept the data between `/challenge/pwn` and `/challenge/college` using `tee` to see what `/challenge/pwn` outputs, which will reveal what it needs from you. Then, use this information to complete the challenge and obtain the flag.

### Concepts Learned
- **Pipe Operator (`|`)**: Connects the standard output of one command to the standard input of another.  
- **Tee Command**: Duplicates data from stdin to both stdout and files, allowing you to intercept and inspect data in a pipeline.  

### Steps to Get the Flag
1. Run the following command to intercept the data from `/challenge/pwn` before it is piped to `/challenge/college`:  
   ```bash
   /challenge/pwn | tee /dev/stdout | /challenge/college
   ```  
   This will display the output of `/challenge/pwn` on the terminal (via `tee /dev/stdout`) while also passing it to `/challenge/college`.  

2. The output from `/challenge/pwn` will contain information about what it needs from you (e.g., a specific input or action). Based on this, you may need to adjust your approach. For example, if `/challenge/pwn` requires a specific string, you might need to provide it by modifying the command or running another instance with the required input.  

3. After providing the necessary input or following the instructions from the intercepted data, `/challenge/college` will process the data and output the flag.  

This demonstrates how to use `tee` for real-time data interception in pipelines, which is useful for debugging and understanding data flow between commands.

---

## Process substitution for input
### Challenge Description  
Use process substitution with `diff` to compare the outputs of `/challenge/print_decoys` and `/challenge/print_decoys_and_flag` to find the real flag.

### Concepts Learned
- **Process Substitution**: Uses `<(command)` syntax to treat command output as temporary files  
- **Comparing Command Outputs**: `diff` can compare the outputs of two commands without creating intermediate files  
- **Flag Identification**: The real flag will appear as the additional line in `/challenge/print_decoys_and_flag` compared to `/challenge/print_decoys`  

### Steps to Get the Flag
1. Run `diff` with process substitution to compare the two command outputs:  
   ```bash
   diff <(/challenge/print_decoys) <(/challenge/print_decoys_and_flag)
   ```  
2. The output will show that `/challenge/print_decoys_and_flag` has an additional line containing the real flag, indicated by something like:  
   ```
   100a101
   > pwn.college{real_flag_here}
   ```  

This demonstrates how process substitution enables direct comparison of command outputs without temporary files.

---

## Writing to multiple programs
### Challenge Description  
Duplicate the output of `/challenge/hack` as input to both `/challenge/the` and `/challenge/planet` using process substitution with `tee`.

### Concepts Learned
- **Process Substitution for Output**: Uses `>(command)` syntax to treat command input as temporary files  
- **Tee with Process Substitution**: `tee` can write to multiple commands simultaneously using process substitution  
- **Data Duplication**: Single input stream can be distributed to multiple commands  

### Steps to Get the Flag
1. Run `/challenge/hack` and pipe its output to `tee` with two process substitutions:  
   ```bash
   /challenge/hack | tee >(/challenge/the) >(/challenge/planet)
   ```  
2. This will:  
   - Execute `/challenge/hack` and capture its output  
   - `tee` duplicates this output to both `/challenge/the` and `/challenge/planet`  
   - Both commands process the same input data simultaneously  
3. The flag will be displayed by one or both of the destination commands  

**Note**  
Process substitution creates temporary named pipes (`/dev/fd/63`, `/dev/fd/64`) that connect the output of `tee` to the input of the specified commands, enabling efficient data distribution without intermediate files.

---

## Split-piping stderr and stdout
To complete this challenge, you need to redirect the standard output (stdout) of `/challenge/hack` to `/challenge/planet` and the standard error (stderr) to `/challenge/the` using process substitution. This ensures that the two streams are processed separately by the respective commands.

### Command
```bash
/challenge/hack > >(/challenge/planet) 2> >(/challenge/the)
```

### Explanation
- `> >(/challenge/planet)` redirects stdout to the input of `/challenge/planet`.
- `2> >(/challenge/the)` redirects stderr to the input of `/challenge/the`.
- This approach keeps stdout and stderr unmixed and directs each to the specified command.

Run this command in the terminal, and the flag will be displayed by one or both of the destination commands.

---

## Named pipes
### Challenge Description  
Create a FIFO (named pipe) at `/tmp/flag_fifo` and redirect the stdout of `/challenge/run` to it. Then, read from the FIFO to receive the flag.

### Concepts Learned
- **FIFOs (Named Pipes)**: Created with `mkfifo`, they allow inter-process communication without disk storage.  
- **Blocking Behavior**: Operations on FIFOs block until both read and write ends are connected.  
- **Dual Terminal Setup**: Required to handle the blocking—one terminal for writing, one for reading.  

### Steps to Get the Flag
1. **Terminal 1 - Create FIFO and Read**:  
   ```bash
   mkfifo /tmp/flag_fifo
   cat /tmp/flag_fifo
   ```  
   This command will block, waiting for data.

2. **Terminal 2 - Write to FIFO**:  
   ```bash
   /challenge/run > /tmp/flag_fifo
   ```  
   This command writes the flag to the FIFO, unblocking Terminal 1, which then displays the flag.

**Note**  
The flag will be displayed in Terminal 1 after executing the write command in Terminal 2. This demonstrates how FIFOs synchronize data flow between processes.
