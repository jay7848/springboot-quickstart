pipeline {
    agent any

    environment {
        APP_DIR = "${WORKSPACE}/springboot-quickstart"
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        stage('Build') {
            steps {
                dir(APP_DIR) {
                    sh 'mvn clean install'
                }
            }
        }
        stage('Test') {
            steps {
                dir(APP_DIR) {
                    sh 'mvn test'
                }
            }
        }
        stage('Package') {
            steps {
                dir(APP_DIR) {
                    sh 'mvn package'
                }
            }
        }
    }

    post {
        success {
            echo "Pipeline completed successfully."
        }
        failure {
            echo "Pipeline failed."
        }
    }
}
