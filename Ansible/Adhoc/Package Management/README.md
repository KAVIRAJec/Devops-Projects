### Package update(apt update & upgrade)

```bash
ansible -i inventory.ini all -m apt -a "update_cache=yes upgrade=dist" --become --private-key ~/private_key.pem
```

This command updates the package cache and performs a distribution upgrade on all hosts in the `inventory.ini` file using the `root` user and a specified SSH private key. `--become` is used to run the command with elevated privileges(sudo).

### Install nginx package

```bash
ansible -i inventory.ini all -m apt -a "name=nginx state=present" --become --private-key ~/private_key.pem
```

### Delete nginx package

```bash
ansible -i inventory.ini all -m apt -a "name=nginx state=absent" --become --private-key ~/private_key.pem
```

### Check service status

```bash
ansible -i inventory.ini all -m service -a "name=nginx state=started" --become --private-key ~/private_key.pem
```

### Check PostgreSQL service status

```bash
ansible -i inventory.ini all -m service -a "name=postgresql state=started" --become --private-key ~/private_key.pem
```

### Start PostgreSQL service

```bash
ansible -i inventory.ini all -m service -a "name=postgresql state=started" --become --private-key ~/private_key.pem
```

to stop the service, change `state=started` to `state=stopped`.
to restart the service, change `state=started` to `state=restarted`.