### Ansible command to get disk usage

```bash
ansible -i inventory.ini all -m shell -a "df -h --private-key ~/private_key.pem"
```

This command checks disk usage on all hosts in the `inventory.ini` file using the `ubuntu` user and a specified SSH private key for authentication.

### Create file
```bash
ansible -i inventory.ini all -m file -a "path=/tmp/testfile state=touch" user=root --private-key ~/private_key.pem
```

This command creates an empty file at `/tmp/testfile` on all hosts in the `inventory.ini` file using the `root` user and a specified SSH private key.

### Create directory
```bash
ansible -i inventory.ini all -m file -a "path=/tmp/testdir state=directory mode=744" user=root --private-key ~/private_key.pem
```
This command creates a directory at `/tmp/testdir` with permissions set to `744` on all hosts in the `inventory.ini` file using the `root` user and a specified SSH private key.

### Copy file
```bash
ansible -i inventory.ini all -m copy -a "src=/path/to/local/file dest=/tmp/testfile owner=root group=root mode=644" --private-key ~/private_key.pem