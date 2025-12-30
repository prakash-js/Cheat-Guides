# Windows Registry
## Registry
  The Windows Registry works like the brain of the Windows operating system. It stores all important configuration information that Windows needs to run properly.
  This includes system settings,hardware details, installed programs, user preferences, and security configurations.
  Windows reads and updates the registry continuously while the system is running.

**HKEY in registry**
  HKEY is primarily a naming convention used by Windows to represent top-level registry handles.

**Hieves**
A registry hive is a file-based database in the Windows Registry that stores a specific set of configuration information and is loaded into memory by Windows during system operation.
(A hive is a registry data file that contains related Windows configuration settings.)

## Windows Registry Hives (Logical View)

| HKEY (Logical Name) | Contains | Backing Hive File / Location |
|--------------------|----------|-----------------------------|
| HKEY_LOCAL_MACHINE (HKLM) | Services, Mounted Devices, Boot Configuration, Drivers, Hardware Information | `SYSTEM` (`C:\Windows\System32\Config\SYSTEM`), `SOFTWARE` (`C:\Windows\System32\Config\SOFTWARE`), `SAM` (`C:\Windows\System32\Config\SAM`), `SECURITY` (`C:\Windows\System32\Config\SECURITY`) |
| HKEY_CURRENT_USER (HKCU) | User Preferences, Recent Files, User-specific Autostart Entries | `NTUSER.DAT` (`C:\Users\<username>\NTUSER.DAT`) |
| HKEY_USERS (HKU) | Settings for all user profiles | `NTUSER.DAT` and `USRCLASS.DAT` for each user (`C:\Users\<username>\...`) |
| HKEY_CLASSES_ROOT (HKCR) | File associations, COM object registrations | Part of `SOFTWARE` hive (`C:\Windows\System32\Config\SOFTWARE`) |
| HKEY_CURRENT_CONFIG (HKCC) | Current hardware configuration | Dynamically generated from `SYSTEM` hive (`C:\Windows\System32\Config\SYSTEM`) |

## Main Registry Operations (CMD)
Windows Registry can be viewed and modified from the Command Prompt using the built-in reg command.
**Core reg commands and syntax**
  * reg query → View registry keys and values

  * reg add → Create or modify registry keys/values

  * reg delete → Remove registry keys or values

**Discover more operations** `reg /?` → Lists all available registry operations and syntax

  * `reg query <reg-key> /f <string>`
  
    /f → Searches for a specified string in value names AND value data
under the given registry key only (not subkeys unless /s is used).

* `reg query <reg-key> /f <string> /s`

  /s -> To search recursively for the particular string

* `reg query <key> /f search.exe /k`

  /k searches only the data (path/content) of a registry value, not the value name (metadata).

*  `reg query <key> /f search.exe /d`

  /d searches inside the value  "**DATA**" (actual stored content), such as the file path stored under a registry key like Run 

*  `reg query <key> /f search.exe /v`

  /v specifies a particular VALUE NAME (the label of the registry entry) to query.

  




