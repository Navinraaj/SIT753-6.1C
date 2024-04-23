pipeline {
    agent any

    environment {
        DIRECTORY_PATH = '/path/to/your/code'
        TESTING_ENVIRONMENT = 'Test'
        PRODUCTION_ENVIRONMENT = 'NavinProduction'
    }

    stages {
        stage('Build') {
            steps {
                echo "Fetch the source code from the directory path specified by the environment variable: ${env.DIRECTORY_PATH}"
                echo "Compile the code and generate any necessary artifacts"
            }
        }

        stage('Test') {
            steps {
                echo "Running unit tests"
                echo "Running integration tests"
            }
        }

        stage('Code Quality Check') {
            steps {
                echo "Check the quality of the code"
            }
        }

        stage('Deploy') {
            steps {
                echo "Deploy the application to a testing environment specified by the environment variable: ${env.TESTING_ENVIRONMENT}"
            }
        }

        stage('Approval') {
            steps {
                script {
                    echo "Waiting for manual approval..."
                    sleep 10 // Pauses the pipeline for 10 seconds simulating an approval step
                }
            }
        }

        stage('Deploy to Production') {
            steps {
                echo "Deploy the code to the production environment: ${env.PRODUCTION_ENVIRONMENT}"
            }
        }
    }

    post {
        always {
            emailext(
                subject: "Jenkins Pipeline Notification for Job: ${env.JOB_NAME}",
                body: """<h1>Pipeline Execution Notification</h1>
                         <p><strong>Job:</strong> ${env.JOB_NAME}</p>
                         <p><strong>Build:</strong> #${env.BUILD_NUMBER}</p>
                         <p><strong>Status:</strong> ${currentBuild.currentResult}</p>
                         <p><strong>Details:</strong> Check the console output <a href="${env.BUILD_URL}console">here</a>.</p>""",
                to: 'navinraaj98@gmail.com'
            )
        }
        failure {
            emailext(
                subject: "Jenkins Pipeline Failure in Job: ${env.JOB_NAME}",
                body: "The build ${env.JOB_NAME} #${env.BUILD_NUMBER} has failed. Check the details at ${env.BUILD_URL}console.",
                to: 'navinraaj98@gmail.com'
            )
        }
    }
}
