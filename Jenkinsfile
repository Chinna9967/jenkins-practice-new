pipeline {
    agent { node { label 'AGENT-1' } }
    options {
        timeout(time: 1, unit: 'HOURS')
        ansiColor('xterm')
    }
    // triggers {
    //     cron '*/2 * * * *'
    // }
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
        stage('input section') {
            input {
                message "should we continue"
                ok "yes, we can"
                submitter "kashi"
            }
            steps {
                echo "Hello , ${USER}"
            }
        }
        stage('Deploy') {
            when {
                environment name: 'USER', value: 'kashi'
            }
            steps {
                sh '''
                echo "Deploying"
                ls -ltr
                pwd
                '''
            }
        }
        stage('Parallel Stage') {
 
            parallel {
                stage('Branch A') {
                    steps {
                        echo "On Branch A"
                        sh 'sleep 10'
                    }
                }
                stage('Branch B') {
                    steps {
                        echo "On Branch B"
                        sh 'sleep 10'
                    }
                }
                stage('Branch C') {
                    stages {
                        stage('Nested 1') {
                            steps {
                                echo "In stage Nested 1 within Branch C"
                                sh 'sleep 10'
                            }
                        }
                        stage('Nested 2') {
                            steps {
                                echo "In stage Nested 2 within Branch C"
                                sh 'sleep 10'
                            }
                        }
                    }
                }
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