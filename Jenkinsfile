pipeline {
    agent { node { label 'AGENT-1' } }
    options {
        timeout(time: 1, unit: 'HOURS')
        ansiColor('xterm')
    }

    environment {
        USER = 'kashi'
    }
    stages {
        stage('Build') {
            steps {
                sh '''
                printenv
                echo "Building"
                '''
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