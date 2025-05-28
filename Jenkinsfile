pipeline {
    agent any

    tools {
        maven 'Maven' // Use the exact name from Jenkins Global Tool Configuration
    }

    environment {
        IMAGE_NAME = "janffy1/spring-ecommerce-api:${env.BUILD_NUMBER}"
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/janffy1/spring-ecommerce-api.git'
            }
        }

        stage('Build Maven Project') {
            steps {
                sh 'mvn clean install'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    dockerImage = docker.build("${IMAGE_NAME}")
                }
            }
        }

        stage('Push Docker Image') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub-credentials', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
                    sh 'echo $DOCKER_PASS | docker login -u $DOCKER_USER --password-stdin'
                    sh "docker push ${IMAGE_NAME}"
                }
            }
        }

        stage('Deploy') {
            steps {
                echo "Deploying ${IMAGE_NAME} - Add your deploy commands here (e.g., SSH into EC2 and run Docker commands)"
            }
        }
    }
}

