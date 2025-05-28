pipeline {
    agent any

    tools {
        maven 'maven' // Make sure this matches the Maven name set in Jenkins Global Tool Configuration
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
                    dockerImage = docker.build("janffy1/spring-ecommerce-api:${env.BUILD_NUMBER}")
                }
            }
        }

        stage('Push Docker Image') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub-credentials', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
                    sh 'echo $DOCKER_PASS | docker login -u $DOCKER_USER --password-stdin'
                    sh "docker push janffy1/spring-ecommerce-api:${env.BUILD_NUMBER}"
                }
            }
        }

        stage('Deploy') {
            steps {
                // Add your deployment script here, e.g. SSH to your server and run docker commands
                echo 'Deploy stage - add your deployment commands here'
            }
        }
    }
}
