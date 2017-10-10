pipeline {
    /* agent { docker 'python:3.5.1' } */
    agent any
    stages {
        stage('build') {
            steps {
                sh 'echo "Hello World!"'
                sh '''
                    uname -a
                    date
                '''
                sh 'python --version'
            }
        }
    }
}
