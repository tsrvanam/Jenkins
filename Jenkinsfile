pipeline {
    agent any

    environment {
        GIT_URL    = 'https://github.com/tsrvanam/Jenkins.git'
        BRANCH     = 'main'
        MAVEN_TOOL = 'maven-3.9.14'
    }

    tools {
        maven "${MAVEN_TOOL}"
    }


    stages {
        
        stage('message') {        
            steps {
                echo 'This is the start of the pipeline.'
            }
        }
        
        stage('Checkout') {
            steps {
                git branch: "${BRANCH}",
                    url: "${GIT_URL}"
            }
        }

        stage('Maven Version') {
            steps {
                sh 'mvn -v'
            }
        }

        stage('Trigger Downstream Job') {
            steps {
                build job: 'airtel-prodcopy', 
                      wait: true, 
                      propagate: true
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
