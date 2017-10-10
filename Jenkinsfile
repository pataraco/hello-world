pipeline {
    /* agent { docker 'python:3.5.1' } */
    /* agent any */
    agent {
        /* docker { image 'node:7-alpine' } */
        docker { image 'node:alpine' }
    }
    stages {
        stage('build') {
            environment {
                ATONG_PUB_SSH = credentials('ATONG_PUB_SSH')
            }
            steps {
                sh 'echo "Hello World!"'
                sh '''
                    uname -a
                    date
                '''
                /* sh 'python --version' */ /* python not found in Alpine docker image */
                /* sh 'echo "${env.ATONG_PUB_SSH}"' */
                sh 'echo "$ATONG_PUB_SSH"'
            }
        }
        stage('test') {
            steps {
                sh 'node --version'
            }
        }
    }
    post {
        always {
            echo "All done!  8)"
            /* collect test results and artifacts */
            archive 'build/libs/**/*.jar'  /* grab built artifacts for local analysis/investigation */
            junit 'build/reports/**/*.xml' /* grab test results and let Jenkins track them */
            mail to: 'patrick.raco@comtechtel.com',
                subject: 'Jenkins: Executed Pipeline: ${currentBuild.fullDisplayName}',
                body: 'Pipeline all done: ${env.BUILD_URL}'
        }
        success {
            echo "Pipeline succeeded!  :)"
        }
        unstable {
            echo "Pipeline is unstable.  :/"
        }
        failure {
            echo "Pipeline failed!  :("
        }
        changed {
            echo "Pipeline status changed.  :|"
        }
    }
}
