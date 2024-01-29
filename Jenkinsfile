pipeline {
    agent any
    
    stages {
        stage('Checkout') {
            steps {
                // Checkout your Magento 2.4.2 project from version control
                checkout scm
            }
        }
        
        stage('Build') {
            steps {
                // Install Magento and build assets
                sh 'composer install'
                sh 'bin/magento setup:upgrade'
                sh 'bin/magento setup:di:compile'
                sh 'bin/magento setup:static-content:deploy -f'
            }
        }
        
        stage('Test') {
            steps {
                // Run automated tests (replace with your actual test commands)
                sh 'bin/magento dev:tests:run unit'
                sh 'bin/magento dev:tests:run integration'
            }
        }
        
        stage('Deploy') {
            steps {
                // Deploy the Magento application (replace with your deployment commands)
                sh 'rsync -avz --delete ./ <remote_server>:<remote_path>'
            }
        }
    }
    
    post {
        always {
            // Clean up steps (optional)
            sh 'composer clear-cache'
        }
    }
}
