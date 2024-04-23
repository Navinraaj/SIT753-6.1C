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
            script {
                def jobName = env.JOB_NAME
                def buildNumber = env.BUILD_NUMBER
                def pipelineStatus = currentBuild.result ?: 'UNKNOWN'
                def bannerColor = pipelineStatus.toUpperCase() == 'SUCCESS' ? 'green' : 'red'

                def body = """<html>
                                <body>
                                    <div style="border: 4px solid ${bannerColor}; padding: 10px;">
                                        <h2>${jobName} - Build ${buildNumber}</h2>
                                        <div style="background-color: ${bannerColor}; padding: 10px;">
                                            <h3 style="color: white;">Pipeline Status: ${pipelineStatus.toUpperCase()}</h3>
                                        </div>
                                        <p>Check the <a href="${env.BUILD_URL}console">console output</a>.</p>
                                    </div>
                                </body>
                              </html>"""

                emailext(
                    subject: "${jobName} - Build ${buildNumber} - ${pipelineStatus.toUpperCase()}",
                    body: body,
                    to: 'navinmachinelearning@gmail.com',
                    from: 'navinraaj@example.com',
                    replyTo: 'navinraaj@example.com',
                    mimeType: 'text/html',
                    attachmentsPattern: '*.txt' // Attachments pattern to attach files if any
                )
            }
        }
    }
}
