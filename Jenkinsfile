pipeline {
    agent any

    environment {
        SSH_KEY_ID = 'jenkins-ssh-key-id'  
    }

    stages {
        stage('Build') {
            steps {
                sh 'echo building'
                sh 'cp env.example .env'
                sh 'pip install -r requirements.txt'
            }
        }
        stage('Test') {
            steps {
               sh 'echo testing'
               sh 'python3 manage.py test'
            }
        }

        stage('Deploy') {
            steps {
                withCredentials([sshUserPrivateKey(credentialsId: SSH_KEY_ID, keyFileVariable: 'SSH_KEY_PATH', usernameVariable: 'SSH_USER')]) {
                    sh """
                    ssh -i $SSH_KEY_PATH -o StrictHostKeyChecking=no $SSH_USER@192.168.1.3 bash /var/www/django/scripts/deploy.sh
                    """
                }
            }
        }
    }
}

