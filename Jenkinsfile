cat > Jenkinsfile << 'EOF'
pipeline {
    agent any

    environment {
        IMAGE_NAME = "myapp"
        IMAGE_TAG = "latest"
    }

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/Shami-12/jenkins-docker'
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
                    sh 'docker rm -f myapp_container || true'
                    sh 'docker run -d --name myapp_container -p 5000:5000 myapp:latest'
                }
            }
        }
    }
}
EOF
