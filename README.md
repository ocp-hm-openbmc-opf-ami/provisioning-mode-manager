# Provisioning Mode Manager

## Introduction

This component is used to manage the `RestrictionMode` property under U-Boot
environment variable using `u-boot-env-mgr`. This property determines the
filtering mechanism which will be applied while executing IPMI commands over
system interface.

## Dependencies

- Boost
- sdbusplus
- phosphor-dbus-interfaces
- phosphor-logging
- Systemd
- CMake
- C++20 compiler

## Design
BMC will restrict the execution of commands based on the following restriction
modes
* `Provisioning` - Allows all command execution through system interface
* `ProvisionedHostAllowlist` - Only allowlist commands will be executed after
  `CoreBiosDone` signal
* `ProvisionedHostDisabled` - No commands are allowed after `CoreBiosDone`
  signal

This component will expose the restriction modes through `RestrictionMode`
property under `xyz.openbmc_project.Control.Security.RestrictionMode` interface.
Also, a redfish event will be logged for any change in restriction mode.

## D-Bus Interfaces

### D-Bus Object Tree

The following object paths are exposed by `xyz.openbmc_project.RestrictionMode.Manager`:

```sh 
`-/xyz
  `-/xyz/openbmc_project
    `-/xyz/openbmc_project/control
      `-/xyz/openbmc_project/control/security
        `-/xyz/openbmc_project/control/security/restriction_mode
```

### D-Bus Introspection

Object path: `/xyz/openbmc_project/control/security/restriction_mode`  
Interface: `xyz.openbmc_project.Control.Security.RestrictionMode`  
Property: `RestrictionMode`  
