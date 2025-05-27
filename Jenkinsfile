pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/janffy1/spring-ecommerce-api.git'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean install'
            }
        }

        // Add Docker and Deploy stages as needed
    }
}
