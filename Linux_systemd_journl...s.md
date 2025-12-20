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


## what is .targets?

systemd target is like a group name that collects related units (services, sockets, mounts) to represent a specific system state. Reaching the target ensures all its member units are started in the correct order.

Some Target name with purpose

| Target                 | Purpose / Use Case                                      |
|------------------------|--------------------------------------------------------|
| multi-user.target      | Standard non-GUI system (servers); most services enable here |
| graphical.target       | GUI environment; use for desktop applications         |
| network.target         | Network stack initialized; use for services that bind to network |
| network-online.target  | Network fully configured (IP ready); use for clients needing connectivity |
| local-fs.target        | Local filesystems mounted; use for disk-dependent services |
| remote-fs.target       | Network filesystems mounted; e.g., NFS-dependent services |
| sysinit.target         | Early system initialization; rarely used directly     |
| basic.target           | Basic system services started; rarely used directly  |


## what is daemon?
daemon is a computer program that runs as a background process rather than under the direct control of an interactive user.

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

View service documentation detail
`systemctl show <unit-name> --property=Documentation`


# Creating Service in Linux 

In Linux systems that use systemd, any executable binary or script can be managed as a service.

To do this, we create a unit file with the extension {filename}.service
  `/etc/systemd/system/{yourservice}.service`
  
A .service file is divided into three logical sections, each with a specific responsibility.

  * [Unit] -> Metadata & ordering.
  * [Service] -> Execution details, core of the service.
  * [Install] -> Boot-time integration.

  
# Required Syntax to Create a systemd Service

## [unit]
```
[Unit]
Description=
After=
Before=
Wants=
Requires=
Documentation=
```
**Description** -> Provides a human-readable description of the service.Displayed in systemctl status.

**After / Before** -> Controls start order, not dependency.we may use After, Before, or accept any valid systemd unit name or .target.

**Example**

```
After=network.target
Before=multi-user.target
```

**Requires** 

Declares a strong dependency.If the required unit fails, your service will fail

**Example**

```
Requires=postgresql.service
```

Documentation -> Links documentation to the service for operators and administrators, it is optional, purely for reference.
**Example**
`
Documentation=man:<command>(<section>)
or
Documentation=<URL>
`

## [Service] 

The [Service] section defines how the service runs, how systemd manages its process, and what happens if it fails. This is the core section of any .service file.
```
[Service]
Type=
ExecStart=/usr/local/bin/myscript.sh
Restart=
RestartSec=
User=
WorkingDirectory=
```

**Type**

Service startup behavior (**simple** is most common )

**ExecStart**

ExecStart is **mandatory** — the absolute path to your executable or script.

**Restart**

Restart=no -> default, never restart

Restart=on-failure -> restart only if process exits with non-zero

Restart=always -> restart no matter how it exits

RestartSec= -> delay before restarting  `RestartSec=80`


**User & Groups**

Defines which Linux **user** and **group** the service process runs as.

**Effect:**  
- The service process inherits the permissions of the specified user and group.  
- Can read/write only files accessible to that user/group.  
- The service’s PID, memory, and created files will be owned by that user and group.

# [Install]

```
[Install]
WantedBy=multi-user.target graphical.target

```

[Install] is optional, but required if you want the service to start automatically at boot.
You usually pair it with WantedBy=multi-user.target for standard services.
Multiple targets can be specified if needed.

## Complete Example Service

**Service File Location:**  
`/etc/systemd/system/myown.service`

**Script / Binary Location:**  
Any valid path (example: `/path/to/executable`)



```ini
[Unit]
Description=My Own Custom Service
After=network.target
Documentation=man:systemd.service(5)

[Service]
Type=simple
ExecStart=/path/to/executable
User=someuser
Group=somegroup
Restart=on-failure
RestartSec=10

[Install]
WantedBy=multi-user.target
```

## After Creating the Service
`sudo systemctl daemon-reload` This command tells the systemd daemon to re-scan and reload service files.When we create or edit a unit files, systemd does not automatically notice the change.

`sudo systemctl start <servicename>` Start immediately the created service.

`sudo systemctl enable <servicename>`  This command enables the service to start automatically at boot.




