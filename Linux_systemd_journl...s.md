#  **Systemd**

Systemd is the init (first process started by the kernel, PID 1) system and service manager used in modern Linux operating systems.
After the Linux kernel boots, it starts /sbin/init as the first user-space process which on modern systems is a symlink to the systemd binary(/lib/systemd/systemd).
Systemd initializes the system, starts and manages services, handles dependencies, monitors processes, and provides tools such as systemctl (service control) and journald (logging).

## What is a Symlink? 

A symbolic link (symlink) is a special file that points to another file or directory.
It works like a shortcut, redirecting access from one path to the actual file.

`ln -s <source> <where_the_shortcut_is_created>`

* ln -s creates a shortcut

* source -> the real file or directory (target)

* where_the_shortcut_is_created ->  the symlink (shortcut)

* Any changes made through the shortcut (symlink) are reflected in the original file or directory.

* When we execute a shortcut (symlink), the system actually executes the source file it points to.

# systemctl
systemctl is the command-line tool used to control and manage services and system state on Linux systems that use systemd.
It is used to manage and inspect systemd units, including 
  - service -> background programs (sshd, tor)
  - socket  -> socket-based activation
  - timer  -> scheduled tasks (cron alternative)  
  - mount -> filesystems
  - target -> boot states (runlevels replacement)
