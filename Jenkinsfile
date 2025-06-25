pipeline {
    agent any

    environment {
        SSH_KEY_ID = 'ansible-key' // Jenkins credential ID
        USER = 'azureuser'
    }

    stages {
        stage('Terraform Init & Apply') {
            steps {
                dir('terraform') {
                    sh 'terraform init'
                    sh 'terraform apply -auto-approve'
                }
            }
        }

        stage('Get VM IP') {
            steps {
                dir('terraform') {
                    script {
                        env.VM_IP = sh(script: "terraform output -raw public_ip", returnStdout: true).trim()
                        echo "VM Public IP: ${env.VM_IP}"
                    }
                }
            }
        }

        stage('Run Ansible Playbook') {
            steps {
                dir('ansible') {
                    sshagent (credentials: [env.SSH_KEY_ID]) {
                        sh "ansible-playbook -i '${VM_IP},' install_web.yml --user ${USER} --ssh-common-args='-o StrictHostKeyChecking=no'"
                    }
                }
            }
        }

        stage('Verify Deployment') {
            steps {
                sh "curl http://${VM_IP}"
            }
        }
    }
}
