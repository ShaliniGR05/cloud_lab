pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/ShaliniGR05/cloud_lab.git'
            }
        }

        stage('Build') {
            steps {
                sh 'echo Building...'
            }
        }

        stage('Test') {
            steps {
                sh 'echo Testing...'
            }
        }
        stage('Deploy') {
            steps {
                sh '''
                cp -r * /var/www/html/
                '''
    }
}
    }
}