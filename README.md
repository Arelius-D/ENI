# ENI
Easy Network Interface (ENI) - The Non-Destructive Network Interface Manager You've Been Looking For!




# Easy Network Interface (ENI) - Project Instructions

## Project Overview
The **Easy Network Interface (ENI)** is designed to provide users with a user-friendly interface for managing and ensuring their system uses the desired network interface. This utility is particularly useful for users with external NICs or those looking to switch between built-in and external interfaces without modifying or overwriting system defaults. ENI is built to be **non-destructive** and **extensible**, enabling users to configure, manage, and restore network settings with ease.

### Key Features:
- **Setup Primary Network Interface**: Users can define their desired primary network interface.
- **Backup and Restore Defaults**: ENI ensures that users can back up and restore system configurations without altering default services like `NetworkManager` or `systemd-networkd`.
- **Non-Destructive Management**: The utility does not modify or replace system defaults but instead works alongside existing configurations.
- **Future-Proof Design**: The tool is modular, allowing future extensions for fallback mechanisms and full Wi-Fi support.

---

## Current Functionality
ENI currently supports the following functionalities:

1. **Check Current Network Configuration**:
   - Detects which service (e.g., `NetworkManager`, `systemd-networkd`, or others) manages the network.
   - Provides the current status of services (e.g., `started`, `enabled`, or both).
   - Optionally allows users to back up this information in a detailed log file within a backup directory (`/etc/eni_backup`).

2. **Backup System Defaults**:
   - Captures the system’s default network configuration (service states, active interfaces, etc.).
   - Creates a snapshot that users can later restore.
   - Does not alter any service or configuration while taking the backup.

3. **Restore System Defaults**:
   - Compares the current configuration with the saved backup.
   - Prompts users twice for confirmation before restoring any changes.
   - Keeps the backup intact for future use.

4. **Setup Easy Network Interface (ENI)**:
   - Guides users through defining their desired primary network interface.
   - Utilizes a non-destructive approach that coexists with system defaults.

5. **Manage Configured Interface**:
   - Allows users to monitor and manage the network interface configured via ENI.
   - Provides simple tools for checking status, link, and other metrics.

6. **Wi-Fi Detection (Foundation)**:
   - Detects active Wi-Fi interfaces (e.g., `wlan0`).
   - Notifies users that Wi-Fi fallback is not supported in the current version.

---

## Updated Instructions for TUI
The text-based user interface (TUI) has been designed to be simple and intuitive. It supports the following options:

### Main Menu
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

### Detailed Steps for Each Option
1. **Check Current Network Configuration**:
   - Displays the service managing the network and its state.
   - Offers to create a backup of this information.
   - Logs the service’s state (e.g., `started` but not `enabled`) to ensure accurate system understanding.

2. **Backup System Defaults**:
   - Saves the current system configuration to `/etc/eni_backup`.
   - Includes a detailed log file documenting service states, active interfaces, and other details.

3. **Restore System Defaults**:
   - Compares the current configuration with the backup.
   - Prompts the user twice before applying any restoration.
   - Leaves the backup intact for future use.

4. **Setup ENI**:
   - Guides users to define and set up their desired primary network interface.
   - Includes logic for validating the selected interface and ensuring non-destructive configuration.

5. **Manage Configured Interface**:
   - Provides basic tools to check the status, link, and other metrics of the configured interface.
   - Ensures no changes are made to system defaults during management.

---

## Future Enhancements
1. **Wi-Fi Fallback Support**:
   - Automate switching to a fallback interface (e.g., from Ethernet to Wi-Fi) if the primary interface loses its link.

2. **Full Wi-Fi Management**:
   - Support for configuring and managing Wi-Fi NICs, including SSID and password settings.

3. **Periodic Status Checks**:
   - Add periodic checks to monitor link status and switch interfaces as needed.

4. **Improved Logs and Analytics**:
   - Provide more detailed analytics and logs for network configurations and statuses.

---

## Notes for Developers
1. **Versioning**:
   - Each code block must include its name, version, and a description of its functionality.
   - Updates or alterations must clearly reference the code block name and version, specifying whether it’s a full update or a partial edit.

2. **Non-Destructive Nature**:
   - Ensure no system default configurations or states are altered unless explicitly requested by the user (e.g., during restoration).

3. **Extensibility**:
   - Design modular code that can easily integrate future features.

---
