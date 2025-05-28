pipeline {
    agent any

    tools {
        maven 'Maven'  // Maven tool configured in Jenkins
    }

    environment {
        IMAGE_NAME = "janffy/springboot-ecommerce"
    }

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/janffy1/spring-ecommerce-api.git'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean install'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh "docker build -t $IMAGE_NAME ."
            }
        }

        stage('Docker Login & Push') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
                    sh '''
                       echo $DOCKER_PASS | docker login -u $DOCKER_USER --password-stdin
                       docker push $IMAGE_NAME
                       docker logout
                    '''
                }
            }
        }

        stage('Deploy') {
            steps {
                echo 'Add your deploy commands here (e.g. SSH and run docker container)'
            }
        }
    }
}
