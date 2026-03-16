pipeline {
    agent any

    environment {
        IMAGE_NAME = "myapp"
        IMAGE_TAG = "latest"
    }

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/Shami-12/jenkins-docker.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    docker.build("${IMAGE_NAME}:${IMAGE_TAG}")
                }
            }
        }

        stage('Run Container') {
            steps {
                script {
                    // Stop old container if exists
                    sh 'docker rm -f myapp_container || true'

                    // Run new container
                    sh 'docker run -d --name myapp_container -p 5000:5000 myapp:latest'
                }
            }
        }
    }

    post {
        success {
            echo 'App deployed successfully!'
        }
        failure {
            echo 'Deployment failed.'
        }
    }
}
