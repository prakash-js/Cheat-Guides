# Fundamental Linux Privilege Escalation Cheat guide

* ## Weak file permissions on /etc/shadow
  After obtaining a shell, check whether the current user can access /etc/shadow. This file contains the password hashes for system accounts.

  If the file is accessible, copy the entire line related to the particular user and store it on your attacker machine (hash.txt).

  Use hashcat mode 1800 (sha512crypt) to crack the obtained hash
