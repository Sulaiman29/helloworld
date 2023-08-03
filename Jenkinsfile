pipeline {
    agent any
    
    environment {
        SONARQUBE_SCANNER_HOME = tool 'SonarQubeScanner'
        DOCKER_IMAGE_NAME = 'final-docker'
    }
    
    stages {
        stage('Checkout Code') {
            steps {
                // Replace the repository URL with your actual code repository URL
                checkout([$class: 'GitSCM', branches: [[name: '*/main']], userRemoteConfigs: [[url: 'https://github.com/Sulaiman29/helloworld.git']]])
            }
        }
        
        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('sonarqube-credentials') {
                    sh "${SONARQUBE_SCANNER_HOME}/bin/sonar-scanner"
                }
            }
        }
        
        stage('Build Docker Image') {
            steps {
                // Replace these commands with your actual build commands
                sh "docker build -t ${DOCKER_IMAGE_NAME}:${env.BUILD_NUMBER} ."
                sh "docker tag ${DOCKER_IMAGE_NAME}:${env.BUILD_NUMBER} ${DOCKER_IMAGE_NAME}:latest"
            }
        }
    }
    
    post {
        success {
            echo 'Pipeline successfully executed!'
        }
        failure {
            echo 'Pipeline failed!'
        }
    }
}
