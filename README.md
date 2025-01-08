# This repo contains only README file. 
# To access the Ansible Playbook please contact the author of this repo.
<p align="center">
<img src="https://logos-world.net/wp-content/uploads/2023/06/Kubernetes-Symbol.png" alt="kubernetes image" height="256">
<img src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcQhZqdh8uZdUtuh3Dpq5Fi7OPf3K0XCNUtxLw&s" alt="ansible image" height="256">
<img src="https://upload.wikimedia.org/wikipedia/commons/thumb/9/9e/UbuntuCoF.svg/1024px-UbuntuCoF.svg.png" alt="ubuntu image" height="256">
</p>
# Kubernetes Cluster Initialization with Ansible

This project provides an Ansible playbook designed to initialize a complete Kubernetes cluster on fresh virtual machines. The playbook automates the setup of Kubernetes components, ensuring a consistent and repeatable deployment process. It has been rigorously tested using [Molecule](https://molecule.readthedocs.io/) with Docker, Vagrant, and EC2 instances.

---

## **Features**
- Automates the initialization of a full Kubernetes cluster (master and worker nodes).
- Configures essential Kubernetes components, such as `kubeadm`, `kubelet`, and `kubectl`.
- Supports multiple environments, including Docker containers, Vagrant-managed VMs, and AWS EC2 instances.
- Implements role-based modular design for better reusability and maintainability.
- Tested thoroughly using Molecule.

---

## **Prerequisites**
Before running this playbook, ensure you have the following tools installed:
- **Ansible**: `>=2.13`
- **Molecule**: `>=3.0`
- **Docker**: For local testing with Molecule.
- **Vagrant**: For VM-based testing.
- **AWS CLI**: For managing EC2 instances.

You’ll also need:
- SSH access to the target machines.
- Appropriate permissions for provisioning instances (if using EC2).

---

## **Project Structure**
```plaintext
├── ansible.cfg          # Ansible configuration file
├── inventory/           # Inventory files for different environments
│   ├── development
│   └── production
├── roles/               # Ansible roles
│   ├── common/          # Common setup tasks
│   ├── master/          # Tasks specific to Kubernetes master node
│   └── worker/          # Tasks specific to Kubernetes worker node
├── molecule/            # Molecule test configurations
│   ├── default/         # Default scenario
│   ├── vagrant/         # Vagrant testing scenario
│   └── ec2/             # EC2 testing scenario
├── playbook.yml         # Main playbook to initialize Kubernetes cluster
├── requirements.yml     # Ansible role dependencies
├── README.md            # Documentation (this file)
└── tests/               # Additional test scripts
```

---

## **Usage**

### **1. Clone the Repository**
```bash
git clone <repository-url>
cd <repository-folder>
```

### **2. Install Required Dependencies**
Install Ansible roles from the `requirements.yml` file:
```bash
ansible-galaxy install -r requirements.yml
```

### **3. Configure Inventory**
Define your target hosts in the `inventory/` file. For example:
```ini
[master]
master-node ansible_host=<master-ip> ansible_user=<user>

[worker]
worker-node1 ansible_host=<worker-ip1> ansible_user=<user>
worker-node2 ansible_host=<worker-ip2> ansible_user=<user>
```

### **4. Run the Playbook**
Execute the playbook to set up the cluster:
```bash
ansible-playbook -i inventory/development playbook.yml
```

### **5. Testing with Molecule**
Run Molecule tests to validate the playbook in different environments.

#### **Docker (Default Scenario)**
```bash
molecule test
```

#### **Vagrant**
```bash
molecule test --scenario-name vagrant
```

#### **EC2**
```bash
molecule test --scenario-name ec2
```

---

## **Testing Details**

### **Molecule Scenarios**
- **Default**: Runs tests using Docker containers to validate the roles and tasks.
- **Vagrant**: Spins up VMs using Vagrant and applies the playbook.
- **EC2**: Tests the playbook on AWS EC2 instances, ensuring compatibility with cloud infrastructure.

Each scenario verifies:
- Kubernetes master and worker nodes are properly initialized.
- `kubectl` is configured to manage the cluster.
- Nodes join the cluster successfully.

---

## **Customization**
You can customize the playbook by modifying the following:
- **Variables**: Adjust variables in `group_vars/` or within roles to match your environment.
- **Roles**: Add or modify tasks in the `roles/` directory as needed.
- **Inventory**: Use separate inventory files for development, staging, and production.

---

## **Contributing**
Contributions are welcome! Feel free to open issues, submit pull requests, or suggest improvements.

---

## **License**
This project is licensed under the MIT License. See the `LICENSE` file for more details.

---

## **Acknowledgments**
- [Ansible](https://www.ansible.com/)
- [Molecule](https://molecule.readthedocs.io/)
- [Kubernetes](https://kubernetes.io/)
