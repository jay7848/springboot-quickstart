pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                dir('springboot-quickstart') {  // Correct Directory!
                    sh '''
                    export JAVA_OPTS="-Djdk.util.zip.disableZip64ExtraFieldValidation=true"
                    mvn clean install -Dorg.jenkinsci.plugins.durabletask.BourneShellScript.HEARTBEAT_CHECK_INTERVAL=86400
                    '''
                }
            }
        }
        stage('Test') {
            steps {
                dir('springboot-quickstart') {
                    sh 'mvn test'
                }
            }
        }
        stage('Package') {
            steps {
                dir('springboot-quickstart') {
                    sh 'mvn package'
                }
            }
        }
        stage('Deploy') {
            steps {
                dir('springboot-quickstart') {
                    sh 'java -jar target/*.jar &'
                }
            }
        }
    }

    post {
        success {
            echo 'Pipeline Succeeded!'
        }
        failure {
            echo 'Pipeline Failed.'
        }
    }
}
