pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                echo "Building"
            }
        }
        stage('test') {
            steps {
                echo "Testing"
            }
        }
        stage('Deploy') {
            steps {
                sh '''
                echo "Deploying"
                ls -ltr
                pwd
                '''
            }
        }
    }
    post {
        always {
            echo "i will always try again"
        }
        success {
            echo "run job success"
        }
        failure {
            echo "run job fail"
    }
}