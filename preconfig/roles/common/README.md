# Ansible role - Common

This role is not supposed to be called but rather used to import its internal macros.

## Requirements

* This role requires Ansible variables, therefore do not disable directive `gather_facts`.

## Files, macros and variables.

Files

* `templates/network.j2`

    Variables

    * `common_network.interfaces` - The list of Ansible fact details about target machine interfaces.

    Macros

    * `mac_to_interface(mac)` - Return interface name (e.g. eth0) specified by the MAC address, or an empty string if the interface does not exist.
    * `ip_to_interface(ip)` - Return interface name (e.g. eth0) specified by the IP address, or an empty string if the interface does not exist.
    * `get_inactive_interfaces()` - Return sublist of `common_network.interfaces` with only inactive interfaces.

## Example

Example of the simplest usage.

```yml
- set_fact:
      interface_name: '
          {%- import "roles/common/templates/network.j2" as network with context -%}
          {{ network.ip_to_interface("192.168.0.2") }}'
```
