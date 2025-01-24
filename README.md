# Easy Network Interface (ENI) - Project Instructions

## Project Overview
The **Easy Network Interface (ENI)** is a user-friendly utility designed to manage and ensure your system uses the desired network interface. ENI is particularly useful for users with external NICs or those switching between built-in and external interfaces without modifying or overwriting system defaults. ENI is built to be **non-destructive**, **extensible**, and highly adaptable for various networking needs.

### Key Features:
- **Define Primary Network Interface**: Users can select their desired primary network interface.
- **Backup and Restore**: Provides tools to back up and restore default system network configurations.
- **Non-Destructive Management**: Operates alongside system defaults without modifying or replacing existing configurations.
- **Extensible Framework**: Modular design to accommodate future features like Wi-Fi management and fallback mechanisms.

---

## Requirements
To use ENI, ensure the following dependencies are installed on your system:

1. **NetworkManager CLI (`nmcli`)**:
   - Lightweight and powerful tool for managing network connections via the command line.
   - Installed by default on most major Linux distributions.
   - To install if missing:
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
   - Detects which service (e.g., `NetworkManager`, `systemd-networkd`, or others) manages the network.
   - Displays the current status of services (e.g., `started`, `enabled`).
   - Optionally logs this information in a backup directory.

2. **Backup System Defaults**:
   - Captures the system’s default network configuration (active interfaces, service states, etc.).
   - Saves a snapshot that users can later restore without altering system defaults.

3. **Restore System Defaults**:
   - Restores the system’s network configuration from a previously saved backup.
   - Prompts users for confirmation before applying changes.

4. **Setup Easy Network Interface (ENI)**:
   - Guides users to define and set up their primary network interface.
   - Ensures that the configuration coexists with existing defaults.

5. **Manage Configured Network Interface**:
   - Allows users to monitor and manage the network interface configured via ENI.
   - Displays details like link state, connection status, and more.

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
5 - Manage Configured Network Interface
    (Manage the interface you’ve configured using ENI)
0 - Exit
----------------------------------------
```

### Steps for Each Option:
1. **Check Current Network Configuration**:
   - Displays which service manages the network and its current state.
   - Offers to create a backup of this configuration for later reference.

2. **Backup System Defaults**:
   - Saves the current system configuration to a backup directory.
   - Includes a detailed log file documenting the service state, active interfaces, and more.

3. **Restore System Defaults**:
   - Compares the current configuration with the saved backup.
   - Prompts the user for confirmation before applying changes.

4. **Setup ENI**:
   - Allows users to select their desired primary network interface.
   - Validates the selection and applies it without altering system defaults.

5. **Manage Configured Interface**:
   - Provides tools to check the status, link, and other metrics of the configured interface.
   - Ensures no changes are made to the system defaults during management.

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
