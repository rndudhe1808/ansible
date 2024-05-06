pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                // Checkout your code from Git
                git branch: 'main', url: 'https://github.com/rndudhe1808/ansible.git'
            }
        }
        stage('Nodes Test') {
            steps {
                // Test connectivity to nodes and Ansible ping
                sh 'ping -c 4 192.168.56.130'
                sh 'ping -c 4 192.168.56.132'
                sh 'ansible all -i inventory.yaml -m ping'
            }
        }
        stage('Run Ansible Playbook') {
            steps {
                // Run Ansible playbook
                sh 'ansible-playbook -i inventory.yaml playbook.yaml'
            }
        }
        stage('Check Apache Status') {
            steps {
                // Check Apache status on specific hosts
                sh 'ansible 192.168.56.130 -i inventory.yaml -m shell -a "systemctl status apache2"'
                sh 'ansible 192.168.56.132 -i inventory.yaml -m shell -a "systemctl status apache2"'
            }
        }
    }
}
