[[Linux]] account creation with an attachment to a sudo group for instance, the user's name is `attacker`

```
sudo useradd attacker -G sudo 
```
Then assign a password like this
```
sudo passwd attacker
```
Finally, add `attacker` to the sudoers group will all privileges
```
echo "attacker ALL=(ALL:ALL) ALL" | sudo tee -a /etc/sudoers
```
