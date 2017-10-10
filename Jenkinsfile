pipeline {
    /* agent { docker 'python:3.5.1' } */
    /* agent any */
    agent {
        /* docker { image 'node:7-alpine' } */
        docker { image 'node:alpine' }
    }
    stages {
        stage('build') {
            steps {
                sh 'echo "Hello World!"'
                sh '''
                    uname -a
                    date
                '''
                /* sh 'python --version' */ /* python not found in Alpine docker image */
                environment {
                    ATONG_PUB_SSH = credentials('ATONG_PUB_SSH')
                }
                sh 'echo "$ATONG_PUB_SSH"'
            }
        }
        stage('test') {
            steps {
                sh 'node --version'
            }
        }
    }
}
