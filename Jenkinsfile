pipeline {
    agent any

    tools {
        maven 'Maven'   // Make sure it's capital M as configured in Jenkins
    }

    environment {
        DOCKERHUB_CREDENTIALS = credentials('dockerhub') // ID of your Jenkins credential
        IMAGE_NAME = "janffy/springboot-ecommerce"       // Your Docker Hub repo
    }

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/janffy1/springboot-ecommerce.git'
            }
        }

        stage('Build Maven Project') {
            steps {
                sh 'mvn clean install'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $IMAGE_NAME .'
            }
        }

        stage('Push Docker Image') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
                    sh '''
                        echo "$DOCKER_PASS" | docker login -u "$DOCKER_USER" --password-stdin
                        docker push $IMAGE_NAME
                        docker logout
                    '''
                }
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deployment step goes here (e.g., SSH into server and run Docker container)'
            }
        }
    }
}
