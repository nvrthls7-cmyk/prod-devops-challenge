pipeline {
    agent any

    tools {
        jdk 'jdk'
        maven 'maven'
        nodejs 'nodejs'
    }

    environment {
        SCANNER_HOME = tool 'sonarqube'
        DOCKER_BIN = '/usr/bin/docker'
        BACKEND_IMAGE = 'sufi0/prod-devops-backend'
        FRONTEND_IMAGE = 'sufi0/prod-devops-frontend'
    }

    stages {

        stage('Git Checkout') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/nvrthls7-cmyk/prod-devops-challenge.git'
            }
        }

        stage('Backend Compile') {
            steps {
                dir('backend') {
                    sh 'mvn clean compile'
                }
            }
        }

        stage('SonarQube Analysis (Backend)') {
            steps {
                dir('backend') {
                    sh """
                    $SCANNER_HOME/bin/sonar-scanner \
                    -Dsonar.host.url=http://localhost:9001 \
                    -Dsonar.token=squ_808404d32303a2c222fa1f257ac8e66dc3712b33 \
                    -Dsonar.projectKey=prod-devops-backend \
                    -Dsonar.projectName=prod-devops-backend \
                    -Dsonar.java.binaries=target
                    """
                }
            }
        }

        stage('OWASP Dependency Check (Backend)') {
            steps {
                dir('backend') {
                    dependencyCheck additionalArguments: '--scan .', odcInstallation: 'dp'
                    dependencyCheckPublisher pattern: '**/dependency-check-report.xml'
                }
            }
        }

        stage('Backend Build') {
            steps {
                dir('backend') {
                    sh 'mvn clean package -DskipTests'
                }
            }
        }

        stage('Frontend Build') {
            steps {
                dir('frontend') {
                    sh '''
                        npm install
                        npm run build
                    '''
                }
            }
        }

        stage('SonarQube Analysis (Frontend)') {
            steps {
                dir('frontend') {
                    sh """
                    $SCANNER_HOME/bin/sonar-scanner \
                    -Dsonar.host.url=http://localhost:9001 \
                    -Dsonar.token=squ_808404d32303a2c222fa1f257ac8e66dc3712b33 \
                    -Dsonar.projectKey=prod-devops-frontend \
                    -Dsonar.projectName=prod-devops-frontend \
                    -Dsonar.sources=.
                    """
                }
            }
        }

        stage('OWASP Dependency Check (Frontend)') {
            steps {
                dir('frontend') {
                    dependencyCheck additionalArguments: '--scan .', odcInstallation: 'dp'
                    dependencyCheckPublisher pattern: '**/dependency-check-report.xml'
                }
            }
        }

        stage('Docker Build & Push') {
            steps {
                withCredentials([
                    usernamePassword(
                        credentialsId: '699a886a-f1a8-4632-b0e9-9e5aae1da6e5',
                        usernameVariable: 'DOCKER_USER',
                        passwordVariable: 'DOCKER_PASS'
                    )
                ]) {
                    sh """
                        $DOCKER_BIN login -u $DOCKER_USER -p $DOCKER_PASS

                        $DOCKER_BIN build -t $BACKEND_IMAGE:latest -f backend/Dockerfile backend
                        $DOCKER_BIN push $BACKEND_IMAGE:latest

                        $DOCKER_BIN build -t $FRONTEND_IMAGE:latest -f frontend/Dockerfile frontend
                        $DOCKER_BIN push $FRONTEND_IMAGE:latest
                    """
                }
            }
        }
    }

    post {
        always {
            echo 'Pipeline finished'
        }
    }
}
