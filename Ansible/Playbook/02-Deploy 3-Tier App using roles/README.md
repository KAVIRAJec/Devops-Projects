### Deployment Commands

```bash
# Deploy to development environment
ansible-playbook -i inventory/hosts.ini myapp-playbook.yml -e env=development

# Deploy to production environment  
ansible-playbook -i inventory/hosts.ini myapp-playbook.yml -e env=production

# Deploy only database tier
ansible-playbook -i inventory/hosts.ini myapp-playbook.yml -e env=development --tags database

# Deploy with verbose output
ansible-playbook -i inventory/hosts.ini myapp-playbook.yml -e env=development -v
```