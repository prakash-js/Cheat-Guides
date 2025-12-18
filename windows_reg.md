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
