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

                # Check if any CSS file exists
                if ! find . -name "*.css" | grep -q .; then
                    echo "No CSS files found!"
                    exit 1
                fi

                echo "File structure is correct"

                # ---------- HTML VALIDATION ----------
                echo "Validating HTML..."

                # Check if tidy is installed
                if ! command -v tidy >/dev/null 2>&1; then
                    echo "tidy is not installed! Skipping HTML validation..."
                else
                    tidy -errors index.html

                    if [ $? -ne 0 ]; then
                        echo "HTML validation failed!"
                        exit 1
                    fi

                    echo "HTML validation passed"
                fi
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