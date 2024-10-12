
The "**net localgroup**" command is a [[Windows]] command-line utility used to manage local groups on a computer. Here's a brief overview of its functions:

1. Display local groups: When used without parameters, it lists all the local groups on the computer.

2. View group members: You can see the members of a specific group by adding the group name after the command.

3. Add or remove groups: It allows you to create new local groups or delete existing ones.

4. Modify group membership: You can add or remove users from local groups.

Some common uses include:

- List all local groups: 
```
net localgroup
```
- View members of a specific group: 
```
net localgroup Administrators
```
- Create a new group: 
```
net localgroup NewGroup /add
```
- Delete a group: 
```
net localgroup NewGroup /delete
```
- Add a user to a group: 
```
net localgroup Administrators username /add
```
- Remove a user from a group: 
```
net localgroup Administrators username /delete
```

This command is particularly useful for system administrators managing local user accounts and permissions on Windows systems.