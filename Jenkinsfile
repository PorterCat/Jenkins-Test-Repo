pipeline {
    agent {
        docker {
            image 'gcc:latest'
            args '-v /var/run/docker.sock:/var/run/docker.sock'
        }
    }

    stages {
        stage('Checkout') {
            steps {
                //git url: 'https://github.com/PorterCat/Jenkins-Test-Repo'
                checkout scm
            }
        }

        stage('Build') {
            steps {
                script {
                    def buildResult = sh(script: 'make obj', returnStatus: true)
                    if (buildResult != 0) {
                        error 'Build failed!'
                    }
                }
            }
        }

        stage('Test') {
            steps {
                script {
                    def testResult = sh(script: 'make test', returnStatus: true)
                    if (testResult != 0) {
                        error 'Tests failed!'
                    }
                }
            }
        }
    }

    post {
        success {
            echo 'Build and tests succeeded!'
        }
        failure {
            echo 'Build or tests failed!'
        }
    }
}