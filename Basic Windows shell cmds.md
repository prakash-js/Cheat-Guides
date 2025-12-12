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
   
* `dir` list the files and directories inside directory. 
   * `dir <file/dir> /q` will show the current owner of the file.


* `icacls`  Helps change file or folder permissions and ownership.In NTFS, every object (file/folder/registry key) has exactly one owner.
   * (I) — Inherited - This permission is inherited from the parent folder and automatically applies to all child files/subfolders unless inheritance is disabled.
   * `icacls "<C:\path\to\folder or file>" /setowner username /T` Changes the owner of a file or folder — and applies the change recursively to all subfolders and file and Without **/T** Changes owner only for that folder itself NOT recursive.
   * `icacls <file> /grant <user>:F` - give user <user> full control(F) only for that file or folder no inheritance, for inheritance we must specify inheritance flags
  
      * **Permission Flags**
         * F  -> Full COntrol
         * RX -> Read and Execute
         * R  -> Read
         * w  -> Write
         * D  -> Delete

    * **Inheritance** means child files and subfolders automatically receive the same permissions as their parent folder unless explicitly overridden.
         * (OI) ->  Files inside the folder
         * (OI) ->  Subfolders inside the folder
 
    * Example   icacls <folder> /grant <user>:(OI)(CI)F /T

        /T tells ICACLS to push those inherited permissions down through all existing subfolders
    
         




* `where <that.exe>` -  Searches exe in  PATH directories
* `where.exe /r <Path> <filename>` -  helps to search for a file recursively (/r) under the specified path.


