pipeline {
    agent any

    environment {
        VENV_PATH = "myapp/venv"
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build') {
            steps {
                echo "Building.."
                sh '''
                cd myapp
                python3 -m venv venv
                . venv/bin/activate
                pip install --upgrade pip
                pip install -r requirements.txt
                '''
            }
        }

        stage('Test') {
            steps {
                echo "Testing.."
                sh '''
                cd myapp
                . venv/bin/activate
                python hello.py
                python hello.py --name=Brad
                '''
            }
        }

        stage('Deliver') {
            steps {
                echo "Delivering..."
                sh '''
                echo "Doing delivery tasks..."
                '''
            }
        }
    }

    post {
        always {
            echo "Cleaning up..."
            sh 'rm -rf myapp/venv'
        }
        success {
            echo "Pipeline succeeded!"
        }
        failure {
            echo "Pipeline failed!"
        }
    }
}
