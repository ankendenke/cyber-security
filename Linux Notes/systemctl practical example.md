[[Linux]] Control the systemd system and service manager

Let's use the Apache web server (often called 'apache2' or 'httpd' depending on the distribution) as our specific service for these practical and advanced examples. 
```bash
# 1. Service Management
# Start Apache and enable it to run on boot
sudo systemctl start apache2
sudo systemctl enable apache2

# Check the status, including recent log entries
systemctl status apache2

# 2. Masking and Unmasking
# Mask the Apache service (prevents it from being started)
sudo systemctl mask apache2

# Try to start the masked service (this will fail)
sudo systemctl start apache2

# Unmask the service
sudo systemctl unmask apache2

# 3. Modifying Service Parameters
# Edit the Apache service file
sudo systemctl edit apache2

# Add these lines to modify service behavior:
[Service]
LimitNOFILE=10000
Restart=always
RestartSec=5

# Reload the systemd manager to apply changes
sudo systemctl daemon-reload

# 4. Dependency Management
# View dependencies of Apache
systemctl list-dependencies apache2

# 5. Creating a Custom Service
# Create a new service file
sudo nano /etc/systemd/system/myapp.service

# Add the following content:
[Unit]
Description=My Custom App
After=network.target

[Service]
ExecStart=/usr/local/bin/myapp
Restart=on-failure
User=myappuser

[Install]
WantedBy=multi-user.target

# Reload systemd, enable and start the new service
sudo systemctl daemon-reload
sudo systemctl enable myapp
sudo systemctl start myapp

# 6. Advanced Logging
# View real-time logs for Apache
journalctl -u apache2 -f

# View logs since last boot
journalctl -u apache2 -b

# 7. Performance Analysis
# Check service startup time
systemd-analyze blame | grep apache2

# 8. Security Hardening
# Edit the Apache service to add security options
sudo systemctl edit apache2

# Add these lines:
[Service]
PrivateTmp=true
ProtectSystem=full
NoNewPrivileges=true

# Reload and restart
sudo systemctl daemon-reload
sudo systemctl restart apache2

# 9. Resource Management
# Set CPU and memory limits for Apache
sudo systemctl set-property apache2.service CPUQuota=50%
sudo systemctl set-property apache2.service MemoryLimit=1G

# Apply changes
sudo systemctl daemon-reload

```

1. Service Management: Basic start, enable, and status checking.
2. Masking and Unmasking: How to completely prevent a service from starting.
3. Modifying Service Parameters: Editing service files to change behavior.
4. Dependency Management: Viewing service dependencies.
5. Creating a Custom Service: Writing a systemd service file from scratch.
6. Advanced Logging: Using journalctl for real-time and boot-specific logs.
7. Performance Analysis: Checking service startup time.
8. Security Hardening: Adding security options to a service.
9. Resource Management: Setting CPU and memory limits for a service.

These exercises cover a range of advanced systemctl features and should give you a good foundation for becoming proficient with the tool. 

To practice, you can run these commands on a Linux system with systemd and Apache installed. Remember to replace 'apache2' with 'httpd' if you're using a Red Hat-based system.
