@Library('jenkins-shared-library@main') _

pipeline {
    agent any

    tools {
        jdk 'jdk'
        maven 'maven'
        nodejs 'nodejs'
    }

    stages {
        stage('CI') {
            steps {
                ciPipeline(
                    backendImage: 'sufi0/prod-devops-backend',
                    frontendImage: 'sufi0/prod-devops-frontend'
                )
            }
        }
    }
}
