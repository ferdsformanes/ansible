# Ansible Ad Hoc Command - Show IP Interface Brief

This ad hoc Ansible command connects to a Cisco IOS device and executes the `show ip int brief` command.

## Command

```bash
ANSIBLE_HOST_KEY_CHECKING=False ansible all -i "192.168.1.10," -m cisco.ios.ios_command -a "commands='show ip int brief'" -u <username> -k -c network_cli -e "ansible_network_os=cisco.ios.ios"
```

## Ansible Ad Hoc Command Syntax

```bash
ansible <host-pattern> -i <inventory> -m <module> -a "<module-arguments>" [options]
```

Example:

```bash
ansible all -i "192.168.1.10," -m cisco.ios.ios_command -a "commands='show ip int brief'" -u <username> -k -c network_cli -e "ansible_network_os=cisco.ios.ios"
```

Where:

- `<host-pattern>` - Host, group, or pattern to target (for example: `all`, `cisco`, `routers`).
- `<inventory>` - Inventory file or inline inventory.
- `<module>` - Ansible module to execute.
- `<module-arguments>` - Arguments passed to the module.
- `[options]` - Optional parameters such as `-u`, `-k`, `-c`, and `-e`.

## Parameters

- `ANSIBLE_HOST_KEY_CHECKING=False` - Temporarily disables SSH host key verification for this command. This prevents Ansible from prompting to trust a device's SSH fingerprint the first time it connects. Useful for labs and testing environments.
- `all` - Target all hosts in the inventory.
- `-i "192.168.1.10,"` - Inline inventory containing a single device.
- `-m cisco.ios.ios_command` - Cisco IOS command module.
- `-a "commands='show ip int brief'"` - Command to execute on the device.
- `-u <username>` - SSH username.
- `-k` - Prompt for SSH password.
- `-c network_cli` - Use the network CLI connection plugin.
- `-e "ansible_network_os=cisco.ios.ios"` - Specify Cisco IOS/IOS-XE as the target network operating system.

## What Does ANSIBLE_HOST_KEY_CHECKING=False Do?

Normally, when connecting to a device for the first time, SSH verifies the device's host key:

```text
The authenticity of host '192.168.1.10' can't be established.
Are you sure you want to continue connecting (yes/no)?
```

Ansible may fail with a host key verification error until the key is added to the local `~/.ssh/known_hosts` file.

By prepending:

```bash
ANSIBLE_HOST_KEY_CHECKING=False
```

Ansible skips this verification and connects immediately.

### Advantages

- Useful for labs and testing.
- Convenient when connecting to many new devices.
- Avoids SSH host key prompts.

### Disadvantages

- Less secure because the device identity is not verified.
- Not recommended for production environments.
- Makes man-in-the-middle attacks harder to detect.

### Recommended Usage

For lab environments:

```bash
ANSIBLE_HOST_KEY_CHECKING=False ansible ...
```

For production environments, connect with SSH once and accept the host key:

```bash
ssh <username>@192.168.1.10
```

Then run Ansible normally without disabling host key checking.
