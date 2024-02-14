#app-armor #linux #security #tutorials #guides #sys-admin #snap #snapcraft #ubuntu #popos #distro-agnostic-packaging

#### File Index:
Section 01 = [[#Security - AppArmor]]   .....................................................   *An introduction and broad overview of `app-armor` in linux...*
Section 02 = [[#Using AppArmor]]   ............................................................   *An easy start guide to setting up `app-armor` on a linux system...*
Section 03 = [[#Profiles]]   ............................................................................   *An overview of the 2 types of `app-armor` profile...* 

# Security - AppArmor

- AppArmor is a Linux Security Module implementation of name-based mandatory access controls. AppArmor confines individual programs to a set of listed files and posix 1003.1e draft capabilities.

- AppArmor is installed and loaded by default. It uses _profiles_ of an application to determine what files and permissions the application requires. Some packages will install their own profiles, and additional profiles can be found in the apparmor-profiles package.

- To install the apparmor-profiles package from a terminal prompt:

```
sudo apt install apparmor-profiles
```

- AppArmor profiles have two modes of execution:
1) ==Complaining/Learning==: profile violations are permitted and logged. Useful for testing and developing new profiles.
2) ==Enforced/Confined==: enforces profile policy as well as logging the violation.

## Using AppArmor

- [i] The optional apparmor-utils package contains command line utilities that you can use to change the AppArmor execution mode, find the status of a profile, create new profiles, etc.

- To install the apparmor-utils package use the following command:

```bash
sudo apt install apparmor-utils
```

- apparmor_status is used to view the current status of AppArmor profiles.
   
```
sudo apparmor_status
```

- aa-complain places a profile into _complain_ mode.
 
```
sudo aa-complain /path/to/bin
```

- aa-enforce places a profile into _enforce_ mode.

```
sudo aa-enforce /path/to/bin
```

- The `/etc/apparmor.d` directory is where the AppArmor profiles are located. It can be used to manipulate the _mode_ of all profiles.
  
Enter the following to place all profiles into complain mode:
 
```bash
sudo aa-complain /etc/apparmor.d/*
```

To place all profiles in enforce mode:
  
```
sudo aa-enforce /etc/apparmor.d/*
```

- apparmor_parser is used to load a profile into the kernel. It can also be used to reload a currently loaded profile using the _-r_ option after modifying it to have the changes take effect.  

- To reload a profile:
 
```
sudo apparmor_parser -r /etc/apparmor.d/profile.name
```

- `systemctl` can be used to _reload_ all profiles:
  
```
sudo systemctl reload apparmor.service
```

- The `/etc/apparmor.d/disable` directory can be used along with the apparmor_parser -R option to _disable_ a profile.
 
```
sudo ln -s /etc/apparmor.d/profile.name /etc/apparmor.d/disable/

sudo apparmor_parser -R /etc/apparmor.d/profile.name
```

- To _re-enable_ a disabled profile remove the symbolic link to the profile in `/etc/apparmor.d/disable/`. Then load the profile using the _-a_ option.

```
sudo rm /etc/apparmor.d/disable/profile.name cat /etc/apparmor.d/profile.name | sudo apparmor_parser -a
```

- AppArmor can be disabled, and the kernel module unloaded by entering the following:
 
```
sudo systemctl stop apparmor.service
sudo systemctl disable apparmor.service
```

- To re-enable AppArmor enter:
 
```
sudo systemctl enable apparmor.service

sudo systemctl start apparmor.service
```

 >[!Note] Take Note:
Replace _profile.name_ with the name of the profile you want to manipulate. Also, replace `/path/to/bin/` with the actual executable file path. For example for the ping command use `/bin/ping`

## Profiles

- [!] AppArmor profiles are simple text files located in `/etc/apparmor.d/`. The files are named after the full path to the executable they profile replacing the “/” with “.”. For example `/etc/apparmor.d/bin.ping` is the AppArmor profile for the `/bin/ping` command.

- [i] There are two main type of rules used in profiles:
1) _Path entries:_ **detail which files an application can access in the file system.**
2) _Capability entries:_ **determine what privileges a confined process is allowed to use.**

As an example, take a look at `/etc/apparmor.d/bin.ping`:

```
#include <tunables/global>
/bin/ping flags=(complain) {
  #include <abstractions/base>
  #include <abstractions/consoles>
  #include <abstractions/nameservice>

  capability net_raw,
  capability setuid,
  network inet raw,
  
  /bin/ping mixr,
  /etc/modules.conf r,
}
```

- _#include <tunables/global>:_ include statements from other files. This allows statements pertaining to multiple applications to be placed in a common file.
- _/bin/ping flags=(complain):_ path to the profiled program, also setting the mode to _complain_.
- _capability net_raw,:_ allows the application access to the CAP_NET_RAW Posix.1e capability.
- _/bin/ping mixr,:_ allows the application read and execute access to the file.

>[!Abstract] Take Note: 
> After editing a profile file the profile must be reloaded. See above at [Using AppArmor](https://ubuntu.com/server/docs/security-apparmor#loadrules) for details.









