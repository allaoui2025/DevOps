pipeline {
    agent any

    environment {
        DOCKERHUB_CREDENTIALS = credentials('dockerhub-creds')
        IMAGE_NAME = "farid2025/devops-app" // بدّل الاسم حسب الإيماج ديالك
    }

    stages {
        stage('Clone') {
            steps {
              git branch: 'main', url: 'https://github.com/allaoui2025/DevOps.git'

            }
        }

        stage('Build Maven') {
            steps {
                sh 'mvn clean install'
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
                withDockerRegistry([credentialsId: 'dockerhub-creds', url: '']) {
                    echo "🔐 Authenticated with DockerHub using credentials: dockerhub-creds"
                    sh "docker push $IMAGE_NAME"
                }
            }
        }

        stage('Run Docker Container') {
            steps {
                sh "docker run -d -p 8080:8080 $IMAGE_NAME"
            }
        }
    }
}
