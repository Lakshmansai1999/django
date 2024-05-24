pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                sh 'echo building'
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
                sh 'echo deploying'
                sh 'ssh -v lucky@192.168.1.24 -o StrictHostKeyChecking=no "bash /var/www/django/scripts/deploy.sh" '
            }
        }
    }
}
