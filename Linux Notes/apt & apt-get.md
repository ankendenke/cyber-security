#### APT and APT-GET

**apt** - command-line interface.  
apt provides a high-level command line interface for the package management system. It is intended as an end user interface and enables some options better suited for interactive usage by default compared to more specialized APT tools like apt-get and apt-cache.

**apt-get** - APT package handling utility -- command-line interface
**apt-get** is the command-line tool for handling packages, and may be considered the user's "back-end" to other tools using the APT library. Several "front-end" interfaces exist, such as aptitude, synaptic and wajig.

Unless the -h, or --help option is given, one of the commands below must be present:

#### Common Options
*install* <**packagename**>: Install a package.

*remove* <**packagename**>: Remove (uninstall) a package.

*purge* <**packagename**>: Remove a package and its configuration files.

*update* <**packagename**>: Update the repository information.
*upgrade*: <**Update**> all packages.

*autoremove*: Remove libraries and other packages that are no longer required.

#### APT specific Option:
*apt search*: Search for a package name in the repositories. This is the same as apt-cache search

*apt show*: Show information about a package. This is the same as apt-cache show .

*apt list option*: Shows lists of installed or upgradeable packages.
```
sudo apt list --installed | grep packagename # Check if packagename is installed
```
*apt edit-sources*: Directly edits the list of repositories that apt searches in for packages.


