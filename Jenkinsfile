pipeline {
    agent any
    environment {
        ODOO_SERVER = 'ubuntu@35.244.37.43:8080'
        ODOO_PATH = '/opt/odoo18/odoo18'
    }
    triggers {
        githubPush()
    }
    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'main', url: 'https://github.com/Dharmesh195/odoo-18-backend-theme.git'
            }
        }
        stage('Deploy to Odoo') {
            steps {
                sshagent(['odoo-ssh-key']) {
                    sh """
                    ssh $ODOO_SERVER 'cd $ODOO_PATH && git pull'
                    ssh $ODOO_SERVER 'sudo systemctl restart odoo18'
                    """
                }
            }
        }
    }
    post {
        success {
            echo '✅ Deployment successful!'
        }
        failure {
            echo '❌ Deployment failed!'
        }
    }
}
