The "**net user**" command is a [[Windows]] command-line utility used to manage user accounts on a local computer or in a domain environment. Here are its main functions:

1. Display user account information
2. Create new user accounts
3. Modify existing user accounts
4. Delete user accounts

Some common uses of the "net user" command include:

1. Viewing all user accounts: 
```
   net user
```

2. Displaying information about a specific user:
```
   net user username
```

3. Creating a new user account:
```
   net user username password /add
```

4. Changing a user's password:
```
   net user username newpassword
```

5. Enabling or disabling an account:
```
   net user username /active:yes (or /active:no)

```
