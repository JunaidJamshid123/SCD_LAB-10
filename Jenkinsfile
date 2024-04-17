pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {

                echo 'Checking out code from GitHub repository...'
                git 'https://github.com/JunaidJamshid123/SCD_LAB-10.git'
            }
        }

        stage('Dependency Installation') {
            steps {
                echo 'Installing dependencies for the project...'
                bat 'npm install'
            }
        }

        stage('Build Docker Image') {
            steps {
                echo 'Building Docker image...'
                bat 'docker build -t my-reactjs-app:latest .'
            }
        }

        stage('Run Docker Image') {
            steps {
                echo 'Running Docker image...'
                bat 'docker run -d -p 3000:3000 my-reactjs-app:latest'
            }
        }

        stage('Push Docker Image') {
            steps {
                echo 'Pushing Docker image to Docker Hub...'
                withCredentials([string(credentialsId: 'DOCKER_HUB_PASSWORD', variable: 'DOCKER_HUB_PASSWORD')]) {
                    bat 'docker login -u <DOCKER_HUB_USERNAME> -p $DOCKER_HUB_PASSWORD'
                    bat 'docker tag my-reactjs-app:latest <DOCKER_HUB_USERNAME>/my-reactjs-app:latest'
                    bat 'docker push <DOCKER_HUB_USERNAME>/my-reactjs-app:latest'
                }
            }
        }
    }
}
