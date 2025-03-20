pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Deploy using Ansible') {
            steps {
                script {
                    // Run Ansible playbook with local execution
                    sh "ansible-playbook -i 'localhost,' ${WORKSPACE}/deploy.yml --extra-vars 'workspace=${WORKSPACE} ansible_connection=local'"
                }
            }
        }
    }

    post {
        failure {
            echo 'Deployment failed'
        }
        success {
            echo 'Deployment successful'
        }
    }
}
