
### Yellow dog Updater Modified

**YUM** (**Yellow dog Updater Modified**) is an open-source command-line as well as graphical-based package management tool for **RPM** (**RedHat Package Manager**) based [[Linux]] systems.

It allows users and system administrators to easily install, update, remove or search software packages on a system.

**YUM** uses numerous third-party repositories to install packages automatically by resolving their dependencies issues.

***yum install*** <package_name> - Install a program name package_name
***yum remove*** <package_name> - Remove a program name package_name
***yum Update*** <package_name> - Update a program name package_name
***yum list*** <package_name> - Search for the specific package with a name 
***yum search***<package_name> - Search for the package if you have a little info on the name
***yum info***<package_name> -  Get info about the package before installing
***yum list | less*** - Get all the list of available programs in YUM database
***yum list installed | less*** - To list all the installed packages on a system.
***yum provides /etc/httpd/conf/httpd.conf*** - To find out which package a specific file belongs to.
***yum check-update*** - To find how many installed packages on your system have updates available
***yum update*** - To keep your system up-to-date with all security and binary package updates

### Red Hat Package Manager
**RPM** (Red Hot Package Manager) is a software package management system for installing, updating, and removing software packages on [[Linux]]-based systems. Red Hat originally developed it but has been adopted by many other [[Linux]] distributions. RPM packages, often denoted with the ==.rpm== file extension contains all the necessary files, metadata, and scripts required to install and manage software on a [[Linux]] system.
### Basic Syntax of RPM in Linux

The basic syntax of the rpm command is as follows:

rpm options package_name

***rpm -i*** package.rpm -  Install package on your system
***rpm -U*** package.rpm - Upgrade package on your system
***rpm -qa*** - List all package installed on your system
***rpm -q*** package_name - To query or get information on the package
***rpm -V*** package_name - Verify package
***rpm -e*** package_name - Erase or uninstall a package from your system

More details:
1. https://www.geeksforgeeks.org/how-to-use-the-rpm-command-in-linux/
2. https://www.tecmint.com/20-practical-examples-of-rpm-commands-in-linux/

