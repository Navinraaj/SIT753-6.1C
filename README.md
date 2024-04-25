# Project Title

SIT753 Credit Task

## Jenkins Pipeline Overview

This repository includes a Jenkinsfile which defines our Continuous Integration/Continuous Deployment (CI/CD) pipeline. The pipeline consists of several stages that are executed in order whenever changes are committed to the repository.

### Pipeline Stages

- **Build**: Compile the code and generate artifacts.
- **Test**: Execute unit tests and integration tests to verify functionality.
- **Code Quality Check**: Analyze code quality using static analysis tools.
- **Security Scan**: Run security scans to identify vulnerabilities.
- **Deploy to Staging**: Deploy the application to a staging environment for further testing.
- **Integration Tests on Staging**: Run additional tests in a staging environment that simulates production.
- **Deploy to Production**: Deploy the application to the production environment.

### Pipeline Triggers

The Jenkins pipeline is triggered by a poll SCM mechanism, which checks the GitHub repository for changes every minute.

### Prerequisites

To use this Jenkins pipeline, you must have the following tools and plugins installed on your Jenkins server:

- Git and a GitHub account
- Jenkins with the following plugins installed:
  - Pipeline
  - Git plugin
  - Email Extension plugin (for notifications)

## Getting Started

To set up this project and pipeline:

1. Fork this repository to your GitHub account.
2. Clone the repository to your local machine.
3. Make changes to the codebase and push them to your GitHub repository.
4. Configure a Jenkins job to point to your repository and use the provided Jenkinsfile.

## Notifications

The pipeline is configured to send email notifications at the end of the 'Test' and 'Security Scan' stages, as well as upon the completion of the pipeline. Notifications will be sent to the configured email address with details of the build status.

## Additional Notes

- Make sure to configure your Jenkins server's SMTP settings to send out emails.
- Adjust the Jenkinsfile environment variables to match your deployment targets.

## Contributing

Contributions to this project are welcome. Please fork the repository, make changes, and submit a pull request.

## License

MIT Lisense

