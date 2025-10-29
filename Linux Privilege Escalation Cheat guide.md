# Fundamental Linux Privilege Escalation Cheat guide

* ## Weak file permissions on /etc/shadow
  After obtaining a shell, check whether the current user can access /etc/shadow. This file contains the password hashes for system accounts.

  If the file is accessible, copy the entire line related to the particular user and store it on your attacker machine (hash.txt).

  Use hashcat mode 1800 (sha512crypt) to crack the obtained hash
  
  		hashcat -m 1800 <hash> <password.list>


* ## SSH keys 
  Look for private SSH keys (like id_rsa) because these files can authenticate SSH logins as other users — use “find” cmd to search the filesystem for “id_rsa” (and variants), check their permissions,   and if accessible copy the key to attacker machine (keeping it at 600) and attempt SSH with that private key.

  		find / -name id_rsa 2> /dev/null
  		ssh -i id_rsa user@<ip>

* ## Sudo -l Privilege Opportunities
  The sudo -l command lists all the commands the current user is allowed (or not allowed) to run with sudo privileges. It helps identify misconfigurations or privilege escalation opportunities. If a user has permission to run certain commands as root without a password, those can often be abused to gain full system access.

  		sudo -l

  Use GTFOBins [https://gtfobins.github.io](https://gtfobins.github.io) as a quick reference for abusing common binaries — check the SUID, sudo and file read/write tricks for any binary you find.

* ## SUID Binary
  SUID is a special permission bit that allows a user to execute a file with the permissions of the file’s owner instead of their own.
    

  Use chmod with a 4 in front of the normal permission digits.To create one.

		chmod 4744 file
    
		
  To find all files with the SUID bit set, use:

		find / -type f -perm -4000 2>/dev/null
    
		
  SUID shows as an s in the owner’s execute position in ls -l, indicating the file runs with the owner’s permissions.

		rwsr--r--


	(If an unprivileged user runs the file with SUID, it executes with the permissions of the file’s owner (creator))
	
* ## Cron jobs
  Cron jobs are used to run scripts or binaries at specific times. By default, they run with the privilege of their owners and not the current user. While properly configured cron jobs are not      inherently vulnerable, they can provide a privilege escalation vector under some conditions.
  Any user can read the file keeping system-wide cron jobs under /etc/crontab
  
  for example

	  0 2 * * * /home/user/backup.sh

  This means: Run /home/user/backup.sh every day at 2:00 AM.

  		* * * * * /home/user/backup.sh
  This runs /home/user/backup.sh every minute.


  If /home/user/backup.sh is writable by a compromised user, that user could replace it with a malicious script. When cron executes the file, the attacker’s code will run with the privileges of the cron job.
  If the job runs as root (e.g., in root’s crontab or /etc/crontab with root as the user), this can lead to root access; if it runs as a normal user, the attacker will gain that user’s privileges.

  
