The `Get-Acl` command in [[Windows]] PowerShell retrieves the Access Control List (ACL) of a specified file, directory, or other system object. An ACL defines the permissions that users and groups have on a system object, such as files and folders.

### Syntax
```powershell
Get-Acl [-Path] <String[]> [<CommonParameters>]
```

### Example Usage

1. **Retrieving the ACL of a file**:
   ```powershell
   Get-Acl -Path "C:\path\to\file.txt"
   ```
   This retrieves the access control list for the specified file.

2. **Retrieving the ACL of a folder**:
   ```powershell
   Get-Acl -Path "C:\path\to\folder"
   ```
   This will show the permissions for the folder and its contents.

3. **Saving the ACL to a variable**:
   ```powershell
   $acl = Get-Acl -Path "C:\path\to\file.txt"
   ```
   This stores the ACL of the file into the `$acl` variable for further manipulation.

4. **Viewing the ACL details**:
   ```powershell
   Get-Acl -Path "C:\path\to\file.txt" | Format-List
   ```
   This displays detailed ACL information in a list format.

### Output Information
The `Get-Acl` command outputs an object representing the ACL, which includes properties such as:

- **Owner**: The owner of the file or directory.
- **Group**: The group associated with the object.
- **Access**: The specific permissions granted (e.g., Read, Write, FullControl).

### Use Cases

- **Viewing current permissions**: Useful for inspecting who has what kind of access to system objects.
- **Security auditing**: Helps in auditing permissions in a system to ensure proper access controls are in place.

