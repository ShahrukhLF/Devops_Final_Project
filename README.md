DevOps Final Project: CI/CD with Jenkins, Terraform, Ansible, and Docker

 Project Overview
This project demonstrates a complete DevOps pipeline that automates infrastructure provisioning and web application deployment using Terraform, Ansible, Jenkins, and Docker. The goal is to implement an end-to-end CI/CD workflow where Jenkins, running inside Docker, triggers the provisioning of an Azure VM via Terraform, configures it using Ansible, and deploys a static web application.

 Tools & Technologies
| Tool        | Purpose                                      |
|-------------|----------------------------------------------|
| Docker      | To containerize and run Jenkins              |
| Jenkins     | CI/CD pipeline automation                    |
| Terraform   | Infrastructure provisioning on Azure         |
| Ansible     | Configuration management and app deployment |
| Azure       | Cloud provider for hosting the VM           |
| GitHub      | Version control and Jenkinsfile repository   |

 Pipeline Workflow
1. Jenkins (in Docker) is triggered manually or on push.
2. Terraform creates a complete Azure infrastructure:
   - Resource group
   - Virtual network and subnet
   - Network interface
   - Public IP
   - Linux virtual machine
3. Ansible connects via SSH to:
   - Install Apache web server
   - Deploy a custom static index.html file
4. The web server becomes accessible via the public IP.
5. The pipeline completes with a verification step using curl.

 Project Structure
Devops_Final_Project/
├── ansible/
│   └── install_web.yml          # Ansible playbook to install Apache & deploy site
├── terraform/
│   └── main.tf                  # Terraform configuration for Azure VM setup
├── Jenkinsfile                  # CI/CD pipeline definition
└── README.txt                   # Project documentation (this file)

 Success Criteria
- Jenkins is containerized using Docker and running successfully.
- Terraform provisions Azure VM and related networking components.
- Ansible installs Apache and deploys static site to the VM.
- Static website loads successfully via public IP.
- Jenkins pipeline is fully automated and completes all stages.

 Output Example
VM Public IP: 20.39.47.115
Deployed site accessible at: http://20.39.47.115

 Clean-up Instructions
To avoid cloud charges, remember to destroy the infrastructure:
cd terraform/
terraform destroy -auto-approve

👨‍💻 Author
Shahrukh Karim
DevOps Student | SZABIST
GitHub: @ShahrukhLF

📄 License
This project is for educational purposes only.
