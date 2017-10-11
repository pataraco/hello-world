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
        always {    /* this will always run */
            echo "All done!  8)"
            /* collect test results and artifacts */
            archive 'build/libs/**/*.jar'  /* grab built artifacts for local analysis/investigation */
            mail to: 'patrick.raco@comtechtel.com',
                subject: "Jenkins: Executed Pipeline: ${currentBuild.fullDisplayName}",
                body: "Pipeline all done: ${env.BUILD_URL}"
            hipchatSend room: 'Announcements',
                message: "Jenkins - Raco is messing with Jenkins and every time his Pipeline runs it will display a message here because this room doesn't have enough announcements",
                color: 'PURPLE'
        }
        success {    /* runs when successful */
            echo "Pipeline succeeded!  :)"
            hipchatSend room: 'VMedix Staging',
                message: "Jenkins - Executed Pipeline: ${currentBuild.fullDisplayName} succeeded",
                color: 'GREEN'
        }
        unstable {    /*  runs when marked as unstable */
            echo "Pipeline is unstable.  :/"
        }
        failure {    /* runs if failed */
            echo "Pipeline failed!  :("
            hipchatSend room: 'VMedix Staging',
                message: "@here; Jenkins - Executed Pipeline - Job Name: ${env.JOB_NAME} - Job No. #${env.BUILD_NUMBER} failed",
                color: 'RED'
        }
        changed {    /* runs if state of Pipeline has changed, e.g. previously failed, but now succeeded */
            echo "Pipeline status changed.  :|"
        }
    }
}
