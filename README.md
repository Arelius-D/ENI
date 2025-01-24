# Easy Network Interface (ENI) - Project Instructions

## Project Overview
The **Easy Network Interface (ENI)** is a robust utility designed to help users seamlessly manage their network interfaces. It ensures the correct interface is prioritized for outbound communication and provides essential tools to back up, restore, and configure network settings dynamically.

ENI is particularly useful for systems with multiple NICs (e.g., external and built-in), allowing users to designate a primary interface while ensuring compatibility with existing system configurations. The tool is modular, extensible, and built with a non-destructive philosophy, making it suitable for all Linux users.

### Key Features:
- **Service Creation for Primary Network Interface**:
  - Automatically sets up a `systemd` service to enforce the selected primary interface.
  - Ensures the correct network interface is consistently used on boot.
- **Dependency Management**:
  - Checks for required tools like `nmcli` and prompts users to install missing dependencies dynamically.
- **Backup and Restore**:
  - Provides tools to back up default network configurations and restore them when needed.
- **Non-Destructive Management**:
  - Operates alongside default system configurations without overwriting critical settings.
- **Detailed Logs**:
  - Logs all actions in a structured manner for troubleshooting and review.
- **Error Handling**:
  - Validates user input and ensures system services are managed safely without disruptions.
- **User-Friendly Design**:
  - Includes a simple text-based interface (TUI) for managing all operations.
- **Extensible Framework**:
  - Designed for future additions, such as Wi-Fi management and automated failover mechanisms.

---

## Requirements
To use ENI, ensure the following dependencies are installed on your system:

1. **NetworkManager CLI (`nmcli`)**:
   - A lightweight tool for managing network connections.
   - Installed by default on most Linux distributions.
   - If missing, you can install it using:
     - **Debian/Ubuntu**: `sudo apt install network-manager`
     - **RHEL/CentOS/Fedora**: `sudo yum install NetworkManager`
     - **Arch/Manjaro**: `sudo pacman -S networkmanager`

2. **Bash Shell**:
   - Requires a POSIX-compliant shell (Bash) to execute scripts.

3. **Linux Utilities**:
   - `systemctl`: For managing services.
   - `tar`: For creating and restoring backups.

---

## Current Functionality
ENI provides the following core functionalities:

1. **Check Current Network Configuration**:
   - Detects and displays which network management service (e.g., `NetworkManager`, `systemd-networkd`) is active.
   - Outputs interface statuses, including link state and IP addresses.

2. **Backup System Defaults**:
   - Saves the system’s current network configuration to a backup directory.
   - Includes critical configuration files and service states for restoration.

3. **Restore System Defaults**:
   - Restores the system’s network configuration from a previously saved backup.
   - Prevents accidental overwrites by prompting for confirmation before applying changes.

4. **Setup Easy Network Interface (ENI)**:
   - Allows users to select a primary network interface dynamically.
   - Creates a `systemd` service (`easy.network.interface.service`) to enforce the configuration.
   - Automatically disables conflicting services to ensure seamless operation.

5. **Manage Configured Network Interface**:
   - Monitors and manages the selected primary network interface.
   - Displays metrics such as link state, connection status, and speed.
   - Ensures the user-defined configuration remains intact during runtime.

6. **Service and Dependency Checks**:
   - Verifies critical services (e.g., Docker) are restarted to ensure outbound connectivity.
   - Provides clear prompts if any required dependencies are missing.

---

## How ENI Service Works
### Service Creation (`easy.network.interface.service`):
- ENI generates a custom `systemd` service file to prioritize the selected primary interface.
- This service ensures that the designated interface is activated on boot and deactivates conflicting interfaces.
- The service is automatically enabled and started during setup.

Example Service File:
```
[Unit]
Description=Manage Network Interface: <PRIMARY_INTERFACE>
After=network-online.target
Wants=network-online.target

[Service]
ExecStart=/usr/bin/nmcli device connect <PRIMARY_INTERFACE>
ExecStop=/usr/bin/nmcli device disconnect <PRIMARY_INTERFACE>
Restart=on-failure
RestartSec=5s

[Install]
WantedBy=multi-user.target
```

### Dependency Validation:
During setup, ENI ensures required dependencies like `nmcli` are installed. If missing, it provides platform-specific instructions to guide the user:

- **Debian/Ubuntu**: `sudo apt install network-manager`
- **RHEL/CentOS/Fedora**: `sudo yum install NetworkManager`
- **Arch/Manjaro**: `sudo pacman -S networkmanager`

---

## Usage
ENI uses a text-based user interface (TUI) to guide users through its options. Upon launching, you will see:

```
Easy Network Interface (ENI) - Main Menu
----------------------------------------
1 - Check Current Network Interface Configuration
    (View system network management status and optionally create a backup)
2 - Backup System's Default Network Configuration
    (Save a snapshot of the system's current default network settings for restoration)
3 - Restore System Default Network Configuration
    (Rollback to the system's default state, if a backup exists)
4 - Setup Easy Network Interface (ENI)
    (Define and configure your desired primary network interface)
5 - Establish The Easy Network Interface (ENI) Service
    (Create and activate the ENI systemd service)
0 - Exit
----------------------------------------
```

### Steps for Each Option:
1. **Check Current Network Configuration**:
   - Identifies and displays active network services and interfaces.
   - Offers to log the configuration details for review.

2. **Backup System Defaults**:
   - Creates a compressed archive of critical network configuration files.
   - Saves the archive to the backup directory with a timestamp.

3. **Restore System Defaults**:
   - Locates the most recent backup and restores the configuration.
   - Verifies integrity before applying changes.

4. **Setup ENI**:
   - Prompts the user to select a primary interface (e.g., `eth0`, `eth1`).
   - Validates the choice and updates internal configuration.
   - Ensures no conflicting services are active.

5. **Establish the ENI Service**:
   - Automatically generates and enables the `easy.network.interface.service`.
   - Stops conflicting services (e.g., Docker) temporarily to avoid disruptions.
   - Restarts any critical outbound services to ensure connectivity.
   - Provides feedback on the status of the service after setup.

---

## Logs
All ENI operations are logged for transparency and troubleshooting. Logs are stored in the `logs/` directory, with filenames following the format:

```
logs/eni_<YYYYMMDD>_<HHMM>.log
```

### Examples of Logged Information:
- Network services checked and their statuses.
- User-selected primary interface.
- Actions performed, such as stopping/starting services.
- Errors encountered during operations.

---

## Future Enhancements
ENI is designed to grow with user needs. Planned future features include:

1. **Wi-Fi Management**:
   - Full support for managing Wi-Fi interfaces, including SSID and password configuration.

2. **Wi-Fi Fallback Support**:
   - Automatic switching to a fallback interface (e.g., Wi-Fi) if the primary interface loses its link.

3. **Periodic Status Checks**:
   - Add periodic checks to monitor link status and automatically switch interfaces if needed.

4. **Detailed Logs and Analytics**:
   - Provide comprehensive analytics and logging for network configurations and performance.

---

## Notes for Developers
1. **Versioning**:
   - All scripts and modules include version numbers for easy tracking.
   - Updates must specify whether changes are partial or full.

2. **Non-Destructive Nature**:
   - Ensure no system defaults are altered unless explicitly requested by the user (e.g., during restoration).

3. **Extensibility**:
   - Code must remain modular and future-proof to allow for seamless integration of new features.

---

