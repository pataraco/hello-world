pipeline {
    /* agent { docker 'python:3.5.1' } */
    /* agent any */
    agent {
        docker { image 'node:7-alpine' }
    }
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
        stage('test') {
            steps {
                sh 'node --version'
        }
    }
}
