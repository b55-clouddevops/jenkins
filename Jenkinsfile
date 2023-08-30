pipeline {
    agent any
    environment {                                  // Pipeline Variables : All the stages of the pipeline can use it.
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
            environment {
                BATCH = "b55"
            }
            steps {
                sh "echo Stage Two Demo"
                sh "echo Trainig  Batch is ${BATCH}"
            }
        }
        stage('Stage Three') {
            steps {
                sh "echo Stage Three Demo"
            }
        }
    }
}