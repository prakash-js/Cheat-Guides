# Fundamental Linux Privilege Escalation Cheat guide

* ## Weak file permissions on /etc/shadow
  After obtaining a shell, check whether the current user can access /etc/shadow. This file contains the password hashes for system accounts.

  If the file is accessible, copy the entire line related to the particular user and store it on your attacker machine (hash.txt).

  Use hashcat mode 1800 (sha512crypt) to crack the obtained hash
    - hashcat -m 1800 <hash> <password.list>


* ## SSH keys 
  Look for private SSH keys (like id_rsa) because these files can authenticate SSH logins as other users — use “find” cmd to search the filesystem for “id_rsa” (and variants), check their permissions,   and if accessible copy the key to attacker machine (keeping it at 600) and attempt SSH with that private key.

    - find / -name id_rsa 2> /dev/null
    - ssh -i id_rsa user@<ip>

* ## Sudo -l Privilege Opportunities
  The sudo -l command lists all the commands the current user is allowed (or not allowed) to run with sudo privileges. It helps identify misconfigurations or privilege escalation opportunities. If a user has permission to run certain commands as root without a password, those can often be abused to gain full system access.

   - sudo -l

Use GTFOBins [https://gtfobins.github.io](https://gtfobins.github.io) as a quick reference for abusing common binaries — check the SUID, sudo and file read/write tricks for any binary you find.
