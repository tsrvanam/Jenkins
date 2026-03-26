pipeline {
    agent any

    environment {
        GIT_URL = 'https://github.com/tsrvanam/Jenkins.git'
        BRANCH  = 'main'
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: "${BRANCH}",
                    url: "${GIT_URL}"
            }
        }

        stage('check') {
            steps {
                echo 'This is to test pipeline.'
            }
        }
    }

    post {
        always {
            echo 'Print this always :(:)'
        }
        success {
            echo 'The job is successful :)'
        }
        failure {
            echo 'The job is failed :)'
        }
    }
}
