# Table of Contents

- [Processes and Jobs](#processes-and-jobs)
  - [Listing Processes](#listing-processes)
  - [Killing Processes](#killing-processes)
  - [Interrupting Processes](#interrupting-processes)
  - [Killing Misbehaving Processes](#killing-misbehaving-processes)
  - [Suspending Processes](#suspending-processes)
  - [Resuming Processes](#resuming-processes)
  - [Backgrounding Processes](#backgrounding-processes)
  - [Foregrounding Processes](#foregrounding-processes)
  - [Starting Backgrounded Processes](#starting-backgrounded-processes)
  - [Process Exit Codes](#process-exit-codes)


---

# Processes and Jobs
<p>Computers execute software to get stuff done.
In modern computing, this software is split into two categories: <em>operating system kernels</em> (about which we will learn <a href="/system-security">much later</a>) and <em>processes</em>, which we will discuss here.
When Linux starts up, it launches an <em>init</em> (short for initializer) process that, in turn, launches a bunch of other processes which launch more processes until, eventually, you are looking at your command line shell, which is also a process!
The shell, of course, launches processes in response to the commands you enter.</p>
<p>In this module, we will learn to view and interact with processes in a number of exciting ways!</p>


## Listing Processes
### Challenge Description
Find the randomly named challenge program running in the background using `ps`, then relaunch it by its full path to get the flag.

### Concepts Learned
- **`ps` command**: Lists running processes with options like `-ef` (standard) or `aux` (BSD)  
- **Process Identification**: Use `grep` to filter processes and `awk` to extract the command path  
- **Process Relaunch**: Execute the discovered program path directly  

### Steps to Get the Flag
1. Find the challenge process and extract its full path:  
   ```bash
   ps aux | grep '/challenge/' | grep -v grep | awk '{print $11}' | head -n 1
   ```  
   This command:  
   - Lists all processes (`ps aux`)  
   - Filters for those containing '/challenge/' (`grep '/challenge/'`)  
   - Excludes the grep command itself (`grep -v grep`)  
   - Extracts the command path (`awk '{print $11}'`)  
   - Takes the first result (`head -n 1`)  

2. Run the extracted path to get the flag:  
   ```bash
   /challenge/$(ps aux | grep '/challenge/' | grep -v grep | awk '{print $11}' | head -n 1 | xargs basename)
   ```  
   This executes the challenge program using its discovered name.

**Note**  
- Use `ps -efww` instead of `ps aux` if the output is truncated  
- The challenge program must be running for this method to work  
- This demonstrates process monitoring and program execution via process discovery

---

## Killing Processes
### Challenge Description
Terminate the `/challenge/dont_run` process using `kill` so that `/challenge/run` can execute and provide the flag.

### Concepts Learned
- **`ps` command**: Lists running processes; use `ps -ef` or `ps aux` to find processes.  
- **`grep` command**: Filters output to find specific processes.  
- **`kill` command**: Terminates processes using their PID.  

### Steps to Get the Flag
1. Find the PID of the `dont_run` process:  
   ```bash
   ps -ef | grep dont_run | grep -v grep
   ```  
   The `grep -v grep` excludes the grep command itself from the results.  
   From the output, note the PID (the second column in `ps -ef`).

2. Terminate the process using `kill`:  
   ```bash
   kill [PID]
   ```  
   Replace `[PID]` with the actual process ID from step 1.

3. Run `/challenge/run` to get the flag:  
   ```bash
   /challenge/run
   ```  

This demonstrates how to identify and terminate processes to allow other programs to run.

---

## Interrupting Processes
To complete this challenge, you need to run the `/challenge/run` program and interrupt it using Ctrl-C. This will send an interrupt signal (SIGINT) to the program, causing it to terminate and display the flag.

### Steps:
1. Execute the program:
   ```bash
   /challenge/run
   ```
2. Immediately press **Ctrl-C** on your keyboard to interrupt the program.
3. The program will terminate and output the flag.

This demonstrates how to use Ctrl-C to send an interrupt signal to a running process in the terminal.

---

## Killing Misbehaving Processes
### Challenge Description
Terminate the decoy process that is writing to the FIFO at `/tmp/flag_fifo` so that `/challenge/run` can write the flag to the FIFO without interference.

### Concepts Learned
- **`ps` command**: Lists running processes to identify the decoy process.  
- **`kill` command**: Terminates the decoy process using its PID.  
- **FIFO (Named Pipe)**: A special file that allows inter-process communication; reading from it may show buffered data initially.  

### Steps to Get the Flag
1. **Read from the FIFO in one terminal** (this will block until data is written):  
   ```bash
   cat /tmp/flag_fifo
   ```  

2. **In another terminal, find and kill the decoy process**:  
   - Find the PID of the decoy process:  
     ```bash
     ps -ef | grep /challenge/decoy | grep -v grep
     ```  
     The output will include the PID (second column).  
   - Kill the process:  
     ```bash
     kill [PID]
     ```  
     Replace `[PID]` with the actual process ID.  

3. **Run `/challenge/run` to write the flag to the FIFO**:  
   ```bash
   /challenge/run
   ```  

4. **View the flag** in the first terminal where `cat /tmp/flag_fifo` is running. You may see decoy flags initially due to buffered data, but after a moment, the real flag will appear.

**Note**  
- If the decoy process is not found, ensure you are using `ps -ef` or `ps aux` with `grep` correctly.  
- The FIFO read may block until data is written, so ensure `/challenge/run` is executed after killing the decoy.

---

## Suspending Processes
### Challenge Description
Run `/challenge/run`, suspend it with Ctrl-Z, then run another instance of `/challenge/run` in the same terminal. The second instance will detect the suspended first instance and output the flag.

### Concepts Learned
- **Process Suspension**: Ctrl-Z sends a SIGTSTP signal, suspending a process and returning control to the shell  
- **Job Control**: Suspended processes remain in memory but are not actively executing  
- **Process Detection**: The challenge program checks for other instances of itself running in the same terminal  

### Steps to Get the Flag
1. **Run the first instance of `/challenge/run`**:  
   ```bash
   /challenge/run
   ```  

2. **Immediately suspend it with Ctrl-Z**:  
   - Press **Ctrl-Z** to suspend the process  
   - You'll see output like: `[1]+  Stopped                 /challenge/run`  
   - The process is now suspended in the background  

3. **Run the second instance of `/challenge/run`**:  
   ```bash
   /challenge/run
   ```  

4. **The second instance will detect the suspended first instance and output the flag**

**Note**  
- After completing the challenge, you can resume the suspended process with `fg` (foreground) or `bg` (background), or terminate it with `kill %1`  
- This demonstrates job control and process suspension in Linux

---

## Resuming Processes
### Challenge Description
Suspend the `/challenge/run` process with Ctrl-Z and then resume it with the `fg` command to receive the flag.

### Concepts Learned
- **Process Suspension**: Ctrl-Z sends SIGTSTP, pausing a process and returning control to the shell  
- **Process Resumption**: `fg` command brings a suspended process back to the foreground  
- **Job Control**: Managing multiple processes in a single terminal session  

### Steps to Get the Flag
1. **Run the challenge program**:  
   ```bash
   /challenge/run
   ```  

2. **Suspend the process with Ctrl-Z**:  
   - Press **Ctrl-Z** to suspend the process  
   - You'll see output like: `[1]+  Stopped                 /challenge/run`  
   - Control returns to the shell prompt  

3. **Resume the process with `fg`**:  
   ```bash
   fg
   ```  
   This brings the suspended process back to the foreground and resumes execution  

4. **The program will complete and output the flag**

**Note**  
- You can view suspended jobs with the `jobs` command  
- Multiple jobs can be managed with `fg %1`, `fg %2`, etc., referring to job numbers  
- This demonstrates basic job control for managing multiple processes in a terminal

---

## Backgrounding Processes
### Challenge Description
Run `/challenge/run`, suspend it with Ctrl-Z, resume it in the background with `bg`, then run another instance of `/challenge/run` in the same terminal. The second instance will detect the backgrounded first instance and output the flag.

### Concepts Learned
- **Process Suspension**: Ctrl-Z sends SIGTSTP, pausing a process  
- **Background Execution**: `bg` resumes a suspended process in the background  
- **Process Detection**: The challenge program checks for other running instances of itself  

### Steps to Get the Flag
1. **Run the first instance of `/challenge/run`**:  
   ```bash
   /challenge/run
   ```  

2. **Suspend the process with Ctrl-Z**:  
   - Press **Ctrl-Z** to suspend the process  
   - You'll see: `[1]+  Stopped                 /challenge/run`  

3. **Resume the process in the background**:  
   ```bash
   bg
   ```  
   This resumes execution while keeping the process in the background  

4. **Run the second instance of `/challenge/run`**:  
   ```bash
   /challenge/run
   ```  

5. **The second instance will detect the backgrounded first instance and output the flag**

**Note**  
- Verify the first process is running in the background with `jobs` or `ps`  
- Background processes continue executing but don't receive terminal input  
- This demonstrates how to manage multiple concurrent processes in a single terminal

---

## Foregrounding Processes
### Challenge Description
Run `/challenge/run`, background it, then foreground it again using `fg` to receive the flag.

### Concepts Learned
- **Process Management**: Using job control commands to move processes between foreground and background  
- **Background Execution**: Processes running in background don't receive terminal input  
- **Foreground Restoration**: Bringing background processes back to the foreground  

### Steps to Get the Flag
1. **Run the challenge program in the foreground**:  
   ```bash
   /challenge/run
   ```  

2. **Suspend the process with Ctrl-Z**:  
   - Press **Ctrl-Z** to suspend the process  
   - You'll see: `[1]+  Stopped                 /challenge/run`  

3. **Resume the process in the background**:  
   ```bash
   bg
   ```  
   This resumes execution while keeping the process in the background  

4. **Bring the process back to the foreground**:  
   ```bash
   fg
   ```  
   This returns the process to the foreground where it can interact with the terminal  

5. **The program will detect this sequence and output the flag**

**Note**  
- You can verify the process state with `jobs` at each step  
- This demonstrates the complete job control cycle: foreground → suspend → background → foreground

---

## Starting Backgrounded Processes
### Challenge Description
Run `/challenge/run` in the background using the `&` operator to receive the flag.

### Concepts Learned
- **Background Execution**: Using `&` to start a process directly in the background  
- **Job Control**: Background processes run independently while you retain terminal control  

### Steps to Get the Flag
1. **Run the challenge program in the background**:  
   ```bash
   /challenge/run &
   ```  
   This will:  
   - Start the process in the background  
   - Display the job number and PID (e.g., `[1] 1234`)  
   - Immediately return control to the shell  

2. **The program will run in the background and output the flag**

**Note**  
- You can check background jobs with the `jobs` command  
- Background processes will continue running even if you log out (unless using `nohup` or similar)  
- This demonstrates how to start processes directly in the background without first running them in the foreground

---

## Process Exit Codes
### Challenge Description
Run `/challenge/get-code` to get an exit code, then pass that exit code as an argument to `/challenge/submit-code` to receive the flag.

### Concepts Learned
- **Exit Codes**: Commands return numeric exit codes (0 for success, non-zero for errors)  
- **`$?` Variable**: Contains the exit code of the last executed command  
- **Command Chaining**: Using exit codes to control program flow  

### Steps to Get the Flag
1. **Run the first command to generate an exit code**:  
   ```bash
   /challenge/get-code
   ```  

2. **Capture the exit code and pass it to the second command**:  
   ```bash
   /challenge/submit-code $?
   ```  
   The `$?` variable automatically contains the exit code from the previous command  

3. **The second command will process the exit code and output the flag**

**Note**  
- You can also chain these in one line:  
  ```bash
  /challenge/get-code; /challenge/submit-code $?
  ```  
- Exit codes are typically 0 for success and 1-255 for various error conditions  
- This demonstrates how to use exit codes for inter-process communication
