##  **Systemd**

Systemd is the init (first process started by the kernel, PID 1) system and service manager used in modern Linux operating systems.
After the Linux kernel boots, it starts /sbin/init as the first user-space process which on modern systems is a symlink to the systemd binary(/lib/systemd/systemd).
Systemd initializes the system, starts and manages services, handles dependencies, monitors processes, and provides tools such as systemctl (service control) and journald (logging).
