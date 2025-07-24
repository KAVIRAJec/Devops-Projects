## Configure AWS Credentials and Install Required Packages

### 1. Install AWS CLI
```sh
pip install awscli
```

### 2. Configure AWS Credentials
```sh
aws configure
```
- Enter your:
    - **AWS Access Key ID**
    - **AWS Secret Access Key**
    - **Default region** (e.g., `us-east-1`)
    - **Output format** (e.g., `json`)

### 3. Create Vault File for Secrets
```sh
ansible-vault create vars/vault.yml
```

### 4. Install Required Collections and Python Packages
```sh
ansible-galaxy collection install amazon.aws
pip install boto3 botocore
```

### 5. Verify AWS Credentials
```sh
aws sts get-caller-identity
```

---

## Running Playbooks

### Run for Development Environment
```sh
ansible-playbook -i inventory/hosts.ini aws-vm-playbook.yml -e environment=dev
```

### Run for Production Environment
```sh
ansible-playbook -i inventory/hosts.ini aws-vm-playbook.yml -e environment=prod
```

### Specify Custom Instance Name and Type
```sh
ansible-playbook -i inventory/hosts.ini aws-vm-playbook.yml \
    -e environment=dev \
    -e instance_name=my-web-server \
    -e instance_type=t3.small
```

### Dry Run (Check Mode)
```sh
ansible-playbook -i inventory/hosts.ini aws-vm-playbook.yml -e environment=dev --check
```

### Verbose Output
```sh
ansible-playbook -i inventory/hosts.ini aws-vm-playbook.yml -e environment=dev -vv
```

---

## Cleanup Resources

To delete resources, use the cleanup playbook:
```sh
ansible-playbook -i inventory/hosts.ini cleanup-playbook.yml
```