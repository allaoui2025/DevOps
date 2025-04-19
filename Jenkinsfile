pipeline {
    agent any

    environment {
        DOCKERHUB_CREDENTIALS = credentials('dockerhub-creds') // خاصك تدير هاد الـ credentials فـ Jenkins
        IMAGE_NAME = "farid2025/devops-app" // بدّلها بـ اسم الــ Docker image ديالك
    }

    stages {
        stage('Clone') {
            steps {
                git 'https://github.com/allaoui2025/DevOps.git'
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
                withDockerRegistry([credentialsId: 'dockerhub-creds', url: '']) {
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
