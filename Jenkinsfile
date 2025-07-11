pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                sh '''
                export JAVA_OPTS="-Djdk.util.zip.disableZip64ExtraFieldValidation=true"
                mvn clean install -Dorg.jenkinsci.plugins.durabletask.BourneShellScript.HEARTBEAT_CHECK_INTERVAL=86400
                '''
            }
        }
        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }
        stage('Package') {
            steps {
                sh 'mvn package'
            }
        }
        stage('Deploy') {
            steps {
                sh 'java -jar target/*.jar &'
            }
        }
    }

    post {
        success {
            echo 'Pipeline succeeded!'
        }
        failure {
            echo 'Pipeline failed.'
        }
    }
}
