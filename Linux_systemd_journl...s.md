#  **Systemd**

Systemd is the init (first process started by the kernel, PID 1) system and service manager used in modern Linux operating systems.
After the Linux kernel boots, it starts /sbin/init as the first user-space process which on modern systems is a symlink to the systemd binary(/usr/lib/systemd/systemd or /lib/systemd/systemd).

Systemd initializes the system, starts and manages services, handles dependencies, monitors processes, and provides tools such as systemctl (service control) and journald (logging).

Systemd defines and manages all system unit types (such as services, sockets, timers, devices, and automounts). However, during boot, the init process (systemd running as PID 1) starts only those units that are explicitly configured, enabled for the active target, or triggered by activation mechanisms. All other units remain inactive until required.

### Common directories for systemd  units
`/etc/systemd/system/`
Stores administrator-defined unit files overrides, and enablement symlinks.
This directory has the **highest priority** and is the correct place to create or modify services.


`/run/systemd/system/`
Stores runtime-generated unit files created during boot or at runtime.
Contents are temporary and are lost after a reboot.

`/lib/systemd/system/ (or /usr/lib/systemd/system/)`
Stores vendor-provided default unit files installed by system packages.
These files should not be modified directly.

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

## Service Operations with systemd (via systemctl)
Using systemd, we can perform the following operations on services through the systemctl command:

  - enable -> configure a service to start automatically at boot

- disable -> prevent a service from starting automatically at boot

- start -> start a service immediately (current session only)

- restart -> stop and then start a service again

- stop -> stop a running service

- status -> display the current state and recent logs of a service

Example Sytax:
```
systemctl start <service>
systemctl stop <service>
systemctl restart <service>
systemctl enable <service>
systemctl disable <service>
```
To List the Active and Inactive units

` systemctl list-units --all `

To list all the active units alone

` systemctl list-units  `

We can use the --type option with systemctl to filter and display only the specific unit type we need.

` systemctl list-units  --type=<name_of_the_unit>  `





