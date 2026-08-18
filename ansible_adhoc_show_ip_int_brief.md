# Ansible Ad Hoc Command - Show IP Interface Brief

This ad hoc Ansible command connects to a Cisco IOS device and executes the `show ip int brief` command.

## Command

```bash
ANSIBLE_HOST_KEY_CHECKING=False ansible all -i "192.168.1.10," -m cisco.ios.ios_command -a "commands='show ip int brief'" -u <username> -k -c network_cli -e "ansible_network_os=cisco.ios.ios"
```

## Parameters

- `all` - Target all hosts in the inventory.
- `-i "192.168.1.10,"` - Inline inventory containing a single device.
- `-m cisco.ios.ios_command` - Cisco IOS command module.
- `-a "commands='show ip int brief'"` - Command to execute on the device.
- `-u <username>` - SSH username.
- `-k` - Prompt for SSH password.
- `-c network_cli` - Use the network CLI connection plugin.
- `-e "ansible_network_os=cisco.ios.ios"` - Specify Cisco IOS/IOS-XE as the target network operating system.
