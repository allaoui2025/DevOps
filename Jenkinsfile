pipeline {
    agent any

    environment {
        IMAGE_NAME = "farid2025/devops-app"
    }

    stages {
        stage('Clone') {
            steps {
                git branch: 'main', url: 'https://github.com/allaoui2025/DevOps.git'
            }
        }

        stage('Build Maven') {
            steps {
                sh './mvnw clean package -DskipTests'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh "docker build -t $IMAGE_NAME ."
            }
        }

        stage('Push Docker Image') {
            steps {
                echo "🚀 Preparing to push Docker image to DockerHub..."
                withDockerRegistry(credentialsId: 'dockerhub-creds', url: '') {
                    echo "🔐 Authenticated with DockerHub"
                    sh "docker push $IMAGE_NAME"
                }
            }
        }

        stage('Run Docker Container') {
            steps {
                echo "🚀 Running Docker container locally"
                sh "docker run -d -p 8080:8080 $IMAGE_NAME"
            }
        }
    }
}
