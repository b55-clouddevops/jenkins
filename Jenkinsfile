pipeline {
    agent any
    environment {
        ENV_URL = "pipeline.google.com"
    }
    stages {        
        stage('Stage One') {
            steps {
                sh '''
                    echo Hello World
                    echo Welcome To Jenkins
                    echo Environment URL is ${ENV_URL}
                  
                  '''
            }
        }
        stage('Stage Two') {
            steps {
                sh "echo Stage Two Demo"
            }
        }
        stage('Stage Three') {
            steps {
                sh "echo Stage Three Demo"
            }
        }
    }
}