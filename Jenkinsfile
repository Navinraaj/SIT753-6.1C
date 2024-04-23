pipeline {
    agent any
    triggers {
        pollSCM('H/1 * * * *') // Polls SCM every 1 minutes
    }
    environment {
        DIRECTORY_PATH = '/path/to/your/code'
        TESTING_ENVIRONMENT = 'Test'
        PRODUCTION_ENVIRONMENT = 'NavinProduction'
    }
    stages {
        // Stage 1: Build
        stage('Build') {
            steps {
                echo "Build the code using a build automation tool like Maven."
                // Tool: Maven
                // Actual build command would be something like 'mvn clean install', but is not implemented here.
            }
        }
        // Stage 2: Unit and Integration Tests
        stage('Test') {
            steps {
                echo "Run unit tests and integration tests."
                // Tools: JUnit for unit tests, Selenium or TestNG for integration tests.
            }
        }
        // Stage 3: Code Analysis
        stage('Code Quality Check') {
            steps {
                echo "Analyze code quality and ensure it meets industry standards."
                // Tool: SonarQube
            }
        }
        // Stage 4: Security Scan
        stage('Security Scan') {
            steps {
                echo "Perform a security scan on the code to identify vulnerabilities."
                // Tool: OWASP ZAP or SonarQube
            }
        }
        // Stage 5: Deploy to Staging
        stage('Deploy to Staging') {
            steps {
                echo "Deploy the application to a staging environment like an AWS EC2 instance."
                // Tool: AWS CLI, Jenkins AWS Plugin
            }
        }
        // Stage 6: Integration Tests on Staging
        stage('Integration Tests on Staging') {
            steps {
                echo "Run integration tests in the staging environment."
                // Tools: Selenium or similar to ensure application functions in a production-like environment.
            }
        }
        // Stage 7: Deploy to Production
        stage('Deploy to Production') {
            steps {
                echo "Deploy the application to a production server, such as an AWS EC2 instance."
                // Tool: AWS CLI, Jenkins AWS Plugin
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
