pipeline {
    agent any

    stages {

        stage('Run Job A - Product API') {
            steps {
                script {
                    echo "Running Job A: OnlineStoreProductAPI_Github"
                    def resultA = build job: 'OnlineStoreProductAPI_Github', propagate: false
                    echo "Job A result: ${resultA.result}"

                    if (resultA.result != 'SUCCESS') {
                        error "Stopping pipeline: Job A failed"
                    }
                }
            }
        }

        stage('Run Job B - Rest API') {
            steps {
                script {
                    echo "Running Job B: OnlineStoreRestAPI_Github"
                    def resultB = build job: 'OnlineStoreRestAPI_Github', propagate: false
                    echo "Job B result: ${resultB.result}"

                    if (resultB.result != 'SUCCESS') {
                        error "Stopping pipeline: Job B failed"
                    }
                    error "Manually failing pipeline for testing"
                }
            }
        }

        stage('Run Job C - Tests') {
            steps {
                script {
                    echo "Running Job C: OnlineStoreRestAPI_Test"
                    def resultC = build job: 'OnlineStoreRestAPI_Test', propagate: false
                    echo "Job C result: ${resultC.result}"

                    if (resultC.result != 'SUCCESS') {
                        error "Stopping pipeline: Job C failed"
                    }
                }
            }
        }
    }

    post {
        success {
            echo "✅ PIPELINE SUCCESS: All jobs passed"
        }
        failure {
            echo "❌ PIPELINE FAILURE: One or more jobs failed"
        }
        always {
            echo "ℹ️ Pipeline execution finished"
        }
    }
}
