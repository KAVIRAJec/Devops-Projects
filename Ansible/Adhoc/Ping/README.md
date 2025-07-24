## Ansible Ping Commands

This README provides examples of using Ansible's `ping` module to test connectivity to hosts defined in your inventory. This takes username from the `inventory.ini` file.

### Ping All Hosts

```bash
ansible -i inventory.ini all -m ping
```

This command pings all hosts listed in the `inventory.ini` file to verify Ansible can connect to them.

### Ping Webservers as Ubuntu User

```bash
ansible -i inventory.ini webservers -m ping -u ubuntu
```

This command pings all hosts in the `webservers` group from the `inventory.ini` file, using the `ubuntu` user for the connection.

### Ping a Host by IP Address

```bash
ansible -i 192.168.1.10 -m ping -u ubuntu
```

Replace `192.168.1.10` with the desired host IP address. This command pings the specified IP using the `ubuntu` user.

### Ping with SSH Key

```bash
ansible -i inventory.ini all -m ping -u ubuntu --private-key ~/private_key.pem
```