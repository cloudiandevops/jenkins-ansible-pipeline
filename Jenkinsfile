pipeline {
    agent any

    environment {
        // Define any required environment variables
        ANSIBLE_HOST_KEY_CHECKING = 'False' // Disable host key checking for Ansible
    }

    stages {
        stage('Checkout Code') {
            steps {
                // Checkout the code from your repository
                git branch: 'main', url: 'https://github.com/cloudiandevops/jenkins-ansible-pipeline'
            }
        }

      

        stage('Run Ansible Playbook') {
            steps {
                // Run the Ansible playbook
                sh '''
                ansiblePlaybook credentialsId: 'ansible-credsid', disableHostKeyChecking: true, installation: 'ansible', inventory: '$WORKSPACE/hosts', playbook: '$WORKSPACE/foodapp-install.yml', vaultTmpPath: ''
                '''
            }
        }
    }

    post {
        success {
            echo 'Ansible playbook executed successfully.'
        }
        failure {
            echo 'Ansible playbook execution failed.'
        }
    }
}
