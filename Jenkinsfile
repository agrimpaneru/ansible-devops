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
                    // Run Ansible playbook with Jenkins workspace as an extra variable
                    sh 'ansible-playbook -i /path/to/inventory /path/to/deploy.yml --extra-vars "workspace=${WORKSPACE}"'
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
