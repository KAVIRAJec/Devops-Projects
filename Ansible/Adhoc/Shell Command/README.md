### Shell command to search running db processes

```bash
ansible -i inventory.ini all -m shell -a "ps aux | grep postgres" --become --private-key ~/private_key.pem
```