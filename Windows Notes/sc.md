The `sc qc` command in Windows is used to **query the configuration** of a specified service. It displays detailed information about how a service is set up, including its executable path, start type, dependencies, and more. Here's a breakdown:

### Command Syntax:

Copy

sc qc <ServiceName>

- Replace `<ServiceName>` with the actual name of the service (e.g., `wuauserv` for Windows Update).
    

---

### What It Does:

When you run `sc qc`, it retrieves the **persistent configuration** of a service (settings stored in the registry). Key details include:

1. **SERVICE_NAME**: The internal name of the service.
    
2. **TYPE**: Whether it's a Win32 service, driver, etc.
    
3. **START_TYPE**: How the service starts (e.g., automatic, manual, disabled).
    
4. **ERROR_CONTROL**: How the system reacts if the service fails.
    
5. **BINARY_PATH_NAME**: The path to the service's executable.
    
6. **DEPENDENCIES**: Other services this one depends on.
    
7. **SERVICE_START_NAME**: The account the service runs under (e.g., `LocalSystem`).
    
8. **DISPLAY_NAME**: The user-friendly name shown in tools like Services.msc.
    

---

### Example Usage:

Copy

sc qc wuauserv

#### Sample Output:

Copy

SERVICE_NAME: wuauserv
TYPE               : 20  WIN32_SHARE_PROCESS
START_TYPE         : 4   DISABLED
ERROR_CONTROL      : 1   NORMAL
BINARY_PATH_NAME   : C:\WINDOWS\system32\svchost.exe -k netsvcs -p
LOAD_ORDER_GROUP   :
TAG                : 0
DISPLAY_NAME       : Windows Update
DEPENDENCIES       : rpcss
SERVICE_START_NAME : LocalSystem

---

### Notes:

- **Administrator Privileges**: While querying configurations typically doesn’t require admin rights, modifying settings (e.g., with `sc config`) does.
    
- **Service Name vs. Display Name**: Use the service's internal name (e.g., `wuauserv`), not its display name (e.g., "Windows Update").
    
- **Common Errors**:
    
    - `[SC] OpenService FAILED 1060`: The service name is invalid or doesn’t exist.
        
    - Incorrect syntax (e.g., missing the service name).
        

---

### Related Commands:

- `sc query`: Check the current **status** of a service (running/stopped).
    
- `sc config`: Modify a service's configuration.
    
- `sc start`/`sc stop`: Start or stop a service.