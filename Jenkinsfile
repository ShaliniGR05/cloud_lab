pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/ShaliniGR05/cloud_lab.git'
            }
        }

        stage('Build') {
            steps {
                sh 'echo Building...'
            }
        }

        stage('Test') {
            steps {
                sh '''
                echo "Running Tests..."

                # ---------- FILE CHECK ----------
                echo "Checking required files..."

                if [ ! -f index.html ]; then
                    echo "index.html not found!"
                    exit 1
                fi

                echo "File structure is correct"

                # ---------- HTML VALIDATION ----------
                echo "Validating HTML..."

                # Install tidy if not already installed
                if ! command -v tidy &> /dev/null; then
                    echo "Installing tidy..."
                    sudo apt-get update
                    sudo apt-get install -y tidy
                fi

                tidy -errors index.html

                if [ $? -ne 0 ]; then
                    echo "HTML validation failed!"
                    exit 1
                fi

                echo "HTML validation passed"
                '''
            }
        }

        stage('Deploy') {
            steps {
                sh '''
                rm -rf /var/www/html/*
                cp -r * /var/www/html/
                '''
            }
        }
    }
}