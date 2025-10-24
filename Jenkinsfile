pipeline {
    agent { node { label 'AGENT-1' } }
    options {
        timeout(time: 1, unit: 'HOURS')
        ansiColor('xterm')
    }
    triggers {
        cron (*/2 * * * *)
    }
    environment {
        USER = 'kashi'
    }
    parameters {
        string(name: 'PERSON', defaultValue: 'Mr Jenkins', description: 'Who should I say hello to?')
        text(name: 'BIOGRAPHY', defaultValue: '', description: 'Enter some information about the person')
        booleanParam(name: 'TOGGLE', defaultValue: true, description: 'Toggle this value')
        choice(name: 'CHOICE', choices: ['One', 'Two', 'Three'], description: 'Pick something')
        password(name: 'PASSWORD', defaultValue: 'SECRET', description: 'Enter a password')
    }
    stages {
        stage('env configure') {
            environment {
                AUTH = credentials('ssh-auth')
            }
            steps {
                sh 'printenv'
            }
        }
        stage('Parameters conf') {
            steps {
                echo " hello ${params.PERSON}"
            }
        }
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
}