pipeline {
    agent any

    tools {
        maven 'Maven-3.9.16'
    }

    environment {
        DOCKER_PATH = 'C:\\Users\\kaush\\AppData\\Local\\Programs\\DockerDesktop\\resources\\bin'
    }
    stages {

        stage('Checkout') {
            steps {
                echo 'Checking out source code from GitHub...'
                checkout scm
            }
        }

        stage('Build') {
            steps {
                echo 'Building application using Maven...'
                bat 'mvn clean package'
            }
        }

        stage('Test') {
            steps {
                echo 'Running Maven tests...'
                bat 'mvn test'
            }
        }

        stage('Docker Build') {
    steps {
        echo 'Building Docker image...'
        bat 'set PATH=%DOCKER_PATH%;%PATH% && docker build -t cicd-app .'
    }
}

       stage('Docker Deploy') {
    steps {
        echo 'Deploying Docker container...'
        bat '''
            set PATH=%DOCKER_PATH%;%PATH%
            docker rm -f cicd-container 2>nul
            docker run --name cicd-container cicd-app
        '''
    }
}

    post {
        success {
            echo 'CI/CD Pipeline completed successfully!'
        }

        failure {
            echo 'CI/CD Pipeline failed!'
        }
    }
}