pipeline {
    agent any
    
    environment {
        DEPLOY_PATH = "/home/agrim/deploy"  // Update with your desired deployment path
    }
    
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        
        stage('Deploy with Ansible') {
            steps {
                script {
                    // Generate inventory file
                    writeFile file: 'inventory.ini', text: '[local]\nlocalhost ansible_connection=local'
                    
                    // Run ansible playbook
                    sh 'ansible-playbook -i inventory.ini deploy-playbook.yml -e "workspace=${WORKSPACE} deploy_path=${DEPLOY_PATH}"'
                }
            }
        }
        
        stage('Verify Deployment') {
            steps {
                sh 'docker ps'
                sh 'curl -s http://localhost:5000/ || echo "Backend may still be starting up"'
                sh 'curl -s http://localhost:8000/ || echo "Frontend may still be starting up"'
            }
        }
    }
    
    post {
        success {
            echo 'Deployment completed successfully!'
        }
        failure {
            echo 'Deployment failed!'
        }
    }
}