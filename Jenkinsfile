pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                echo 'Checking out code from GitHub repository...'
                git 'https://github.com/aditya-sridhar/simple-reactjs-app.git'
            }
        }

        stage('Dependency Installation') {
            steps {
                echo 'Installing dependencies for the project...'
                sh 'npm install'
            }
        }

        stage('Build Docker Image') {
            steps {
                echo 'Building Docker image...'
                sh 'docker build -t my-reactjs-app:latest .'
            }
        }

        stage('Run Docker Image') {
            steps {
                echo 'Running Docker image...'
                sh 'docker run -d -p 3000:3000 my-reactjs-app:latest'
            }
        }

        stage('Push Docker Image') {
            steps {
                echo 'Pushing Docker image to Docker Hub...'
                withCredentials([string(credentialsId: 'DOCKER_HUB_PASSWORD', variable: 'DOCKER_HUB_PASSWORD')]) {
                    sh 'docker login -u <DOCKER_HUB_USERNAME> -p $DOCKER_HUB_PASSWORD'
                    sh 'docker tag my-reactjs-app:latest <DOCKER_HUB_USERNAME>/my-reactjs-app:latest'
                    sh 'docker push <DOCKER_HUB_USERNAME>/my-reactjs-app:latest'
                }
            }
        }
    }
}
