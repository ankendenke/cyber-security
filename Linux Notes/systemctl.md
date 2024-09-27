systemctl [[Linux]] is a command-line tool used in Linux systems that use systemd as their init system and service manager. It's used to control and manage systemd, which is responsible for initializing and maintaining system services.

Here are the key points to understand:

1. Purpose:
    - Manages system services and resources
    - Starts, stops, restarts, and checks the status of services
    - Enables or disables services to start at boot
2. Basic syntax: systemctl [command] [unit]
3. Essential commands: 
    a. Check status:
```
    systemctl status [service]
```
    b. Start a service:
```
    sudo systemctl start [service]
```
    c. Stop a service:
```
    sudo systemctl stop [service]
```
    d. Restart a service:
```
    sudo systemctl restart [service]
```
    e. Enable a service to start at boot:
```
    sudo systemctl enable [service]
```
    f. Disable a service from starting at boot:
```
    sudo systemctl disable [service]
```
    g. Reload a service's configuration:
```
    sudo systemctl reload [service]
```
4. Viewing system state:
    - List all units: `systemctl list-units`
    - List all services: `systemctl list-units --type=service`
    - List failed units: `systemctl --failed`
5. System management:
    - Reboot: `sudo systemctl reboot`
    - Shutdown: `sudo systemctl poweroff`
    - Suspend: `sudo systemctl suspend`
6. Viewing logs: Use `journalctl` to view logs. For a specific service:
```
    journalctl -u [service]
```
