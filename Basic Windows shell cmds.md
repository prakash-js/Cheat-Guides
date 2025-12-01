## Windows Shells Overview

In Windows, there are two main environments for running commands: cmd.exe and powershell.exe.


**CMD** is a traditional, text-based command-line interpreter based on MS-DOS. It has been a part of Windows operating systems for decades and offers limited updates.

**PowerShell** is a more powerful and flexible object-oriented shell and scripting language built on the .NET framework. It is actively developed and receives regular updates.


# Some Basic Command in cmd.exe

* `systeminfo`  Displays detailed information about the system.
* `whoami`  Displays the username of the account currently executing the command.
  * `whoami /groups`  it lists all the groups the current user is a member of.
  * `whoami /priv`  Shows the privileges assigned to the current user.



* `cd`  command is used for directory navigation.
  * `cd`              Displays the current directory.
  * `cd ..`           Moves back to the parent directory.
  * `cd <dir-name>`     Enters the specified directory.

* `net accounts` Shows password and login policy settings.
* `ipconfig` Displays basic IP configuration details for all active network adapters.
  * `ipconfig /all` Shows complete network configuration details for all adapters.
  * `ipconfig /?` Displays the help menu for the ipconfig command
    
* `tasklist` Displays a list of all running processes on the system.
   * `tasklist /?` Shows the help menu for tasklist, allowing you to explore additional options that provide more flexibility


* `icacls`  Helps change file or folder permissions and ownership.In NTFS, every object (file/folder/registry key) has exactly one owner.
   * `dir main.cpp /q` 
   * (I) — Inherited - This permission is inherited from the parent folder and automatically applies to all child files/subfolders unless inheritance is disabled.
   * `icacls "C:\path\to\folder" /setowner username /T` Changes the owner of a file or folder — and applies the change recursively to all subfolders and file and Without **/T** Changes owner only for that folder itself NOT recursive.
   * 




* `where <that.exe>` -  Searches exe in  PATH directories


