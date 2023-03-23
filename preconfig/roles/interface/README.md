# Ansible role - Interface

This role serves for network interface configuration on debian-based systems.

## Requirements

* This role requires root access, so you either need to specify `become` directive as a global or while invoking the role.

    ```yml
    become: yes
    ```
    
* Also requires Ansible variables, therefore do not disable directive `gather_facts`.

## Role paramaters

Mandatory parameters.

* `interface_identification` - The identification of the interface to configure. Either the IPv4 address, the MAC address, or the interface name.

Optional parameters.

* `interface_configuration_type` - The type of interface configuration. Either **dhcp**, or **static** (default: **dhcp**).
* `interface_static_ip` - The static IPv4 address of the interface. This value is used only if the `interface_configuration_type` parameter is set to **static**.
* `interface_static_netmask` - The network mask of the `interface_static_ip`. This value is used only if the `interface_configuration_type` parameter is set to **static**.
* `interface_clean` - Boolean value (**True**/**False**) that means whether to clean all interface configuration before applying role or not (default: **True**).
* `interface_default_gateway` - The IPv4 address of default gateway.
* `interface_file_name` - The file name for your configuration located in `/etc/network/interfaces.d/` directory (by default the file `/etc/network/interface` is used).
* `interface_mtu` - The number of maximum transmission unit (default: **1442**).
* `interface_routes` - The list of route parameters. Each route **MUST** consist of following attributes (default: **[]**).
    * `gateway` - The IPv4 address of next hop for this route.
    * `network` - The network IPv4 address of the pakets that will be routed.
    * `netmask` - The subnet mask of the specified `network` in address format or prefix number.

## Example

Example of the simplest network interface configuration that just set MTU of specified interface.

```yml
roles:
    - role: interface
      interface_mac: 01:23:45:67:89:ab
      interface_mtu: 1500
```
