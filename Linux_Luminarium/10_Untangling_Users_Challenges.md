# Untangling Users
<p>Did you think you, <code>hacker</code>, are alone in the workspace?
There are MANY users on a typical Linux system!
The full list of users on a Linux system is specified in the <code>/etc/passwd</code> file (named so for historical reasons --- it doesn't actually hold passwords anymore).
Here is an example from the dojo container:</p>
<pre><code class="language-console hljs shell">root:x:0:0:root:/root:/bin/bash
daemon:x:1:1:daemon:/usr/sbin:/usr/sbin/nologin
bin:x:2:2:bin:/bin:/usr/sbin/nologin
sys:x:3:3:sys:/dev:/usr/sbin/nologin
sync:x:4:65534:sync:/bin:/bin/sync
games:x:5:60:games:/usr/games:/usr/sbin/nologin
man:x:6:12:man:/var/cache/man:/usr/sbin/nologin
lp:x:7:7:lp:/var/spool/lpd:/usr/sbin/nologin
mail:x:8:8:mail:/var/mail:/usr/sbin/nologin
news:x:9:9:news:/var/spool/news:/usr/sbin/nologin
uucp:x:10:10:uucp:/var/spool/uucp:/usr/sbin/nologin
proxy:x:13:13:proxy:/bin:/usr/sbin/nologin
www-data:x:33:33:www-data:/var/www:/usr/sbin/nologin
backup:x:34:34:backup:/var/backups:/usr/sbin/nologin
list:x:38:38:Mailing List Manager:/var/list:/usr/sbin/nologin
irc:x:39:39:ircd:/var/run/ircd:/usr/sbin/nologin
gnats:x:41:41:Gnats Bug-Reporting System (admin):/var/lib/gnats:/usr/sbin/nologin
nobody:x:65534:65534:nobody:/nonexistent:/usr/sbin/nologin
_apt:x:100:65534::/nonexistent:/usr/sbin/nologin
systemd-timesync:x:101:101:systemd Time Synchronization,,,:/run/systemd:/usr/sbin/nologin
systemd-network:x:102:103:systemd Network Management,,,:/run/systemd:/usr/sbin/nologin
systemd-resolve:x:103:104:systemd Resolver,,,:/run/systemd:/usr/sbin/nologin
mysql:x:104:105:MySQL Server,,,:/nonexistent:/bin/false
messagebus:x:105:106::/nonexistent:/usr/sbin/nologin
sshd:x:106:65534::/run/sshd:/usr/sbin/nologin
hacker:x:1000:1000::/home/hacker:/bin/bash
</code></pre>
<p>A lot of users here, and a lot of info!
Each line contains, separated by <code>:</code>s, the username, an <code>x</code> as a placeholder for where the password <em>used</em> to be (we'll cover where it actually is later), the numerical user ID, the numerical default group ID, long-form user details, the home directory, and the default shell.</p>
<p>We can see the <code>hacker</code> user at the bottom.
That's you!
Most of the rest of these users are either there for historical reasons, are service accounts to support various installed software, or some are "utility" accounts (e.g., the <code>nobody</code> user is used to ensure that, e.g., some programs run without any special privileges).</p>
<p>One important user is <code>root</code>: the system administrator.
The system administrator has obvious security implications: a <code>hacker</code> user that can somehow, through various functionalities of Linux, become the <code>root</code> user would be able to wreak havoc on the system.
A very frequent goal of hackers breaking into systems is to escalate to <code>root</code>, and thus <code>root</code> must be defended at all cost!</p>
<p>In this module, we'll explore various user shenanigans, learn the intended ways to switch users to administer the system, and have fun along the way!</p>

---

## Becoming root with su
### Challenge Description
Use the `su` command with the root password "hack-the-planet" to become root and read the flag.

### Concepts Learned
- **`su` command**: Allows switching to another user (commonly root) with proper authentication  
- **Root Access**: Provides full system privileges for accessing protected files  
- **SetUID Binary**: `su` runs with root privileges due to its special permissions  

### Steps to Get the Flag
1. **Run `su` to switch to root**:  
   ```bash
   su
   ```  

2. **Enter the root password when prompted**:  
   ```
   hack-the-planet
   ```  

3. **Once you have root access, read the flag**:  
   ```bash
   cat /flag
   ```  
   Or if the flag is in another location:  
   ```bash
   cat /root/flag
   ```  

**Note**  
- The password will not be visible as you type (standard security behavior)  
- After becoming root, your prompt will change to `root@dojo:/home/hacker#`  
- This demonstrates basic privilege escalation using `su` with a known password

---

## Other users with su
### Challenge Description
Switch to the `zardus` user using `su` with the password "dont-hack-me", then run `/challenge/run` to get the flag.

### Concepts Learned
- **`su` with username**: Allows switching to specific users other than root  
- **User Authentication**: Requires the target user's password  
- **Privilege Context**: Programs run with the privileges of the user you switch to  

### Steps to Get the Flag
1. **Switch to the `zardus` user**:  
   ```bash
   su zardus
   ```  

2. **Enter the password when prompted**:  
   ```
   dont-hack-me
   ```  

3. **Run the challenge program**:  
   ```bash
   /challenge/run
   ```  

4. **The program will output the flag**

**Note**  
- After switching users, your prompt will change to `zardus@dojo:/home/hacker$`  
- You can verify your current user with `whoami`  
- This demonstrates how to switch between user accounts using `su`

---

## Cracking passwords
### Steps to Get the Flag
1. **Crack the password with John the Ripper**:
   ```bash
   john /challenge/shadow-leak
   ```
   This command will start cracking the passwords in the shadow file. It may take a few minutes. Once done, view the cracked password with:
   ```bash
   john --show /challenge/shadow-leak
   ```
   From the output, note the password for `zardus`. In this case, the cracked password is `password1337`.

2. **Switch to the `zardus` user**:
   ```bash
   su zardus
   ```
   When prompted, enter the cracked password: `password1337`.

3. **Run the challenge program**:
   ```bash
   /challenge/run
   ```
   This will output the flag.

### Note:
- Ensure John the Ripper is installed (it should be available in the pwn.college environment).
- The password cracking process might vary in time depending on the complexity of the password.

---

## Using sudo
### Challenge Description
Use `sudo` to execute a command with root privileges and read the flag.

### Concepts Learned
- **`sudo` command**: Allows authorized users to run commands as root or other users  
- **Privilege Escalation**: Temporary elevation of privileges for specific commands  
- **Policy-Based Access**: Controlled by `/etc/sudoers` configuration  

### Steps to Get the Flag
1. **Use `sudo` to read the flag**:  
   ```bash
   sudo cat /flag
   ```  
   This will display the flag if you have sudo privileges.

2. **If the flag is in a different location, adjust the path accordingly**.

**Note**  
- `sudo` typically requires your user password, not the root password  
- This demonstrates modern privilege escalation using `sudo` instead of `su`  
- In pwn.college's Privileged Mode, you'll have full sudo access for debugging purposes
