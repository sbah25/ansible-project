pipeline {
    agent {
        node {
            label 'ansible-controller'
        }
    }

    stages {
        stage('Checkout Code') {
            steps {
                // Check out the Ansible playbook from source control
                checkout scm
            }
        }

        stage('Run Ansible Playbook') {
            steps {
                ansiblePlaybook(
                    credentialsId: 'ansible-ssh',
                    inventory: './inventory',
                    playbook: './web.yaml'
                )
            }
        }
    }

    post {
        always {
            archiveArtifacts artifacts: '*.log', allowEmptyArchive: true
        }

        success {
            echo 'Playbook executed successfully!'
        }

        failure {
            echo 'Playbook execution failed!'
        }
    }
}
