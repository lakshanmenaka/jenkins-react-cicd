pipeline {
    agent any

    environment {
        IMAGE_NAME = 'react-cicd-app'
        CONTAINER_NAME = 'react-cicd-app'
        HOST_PORT = '8081'
        CONTAINER_PORT = '80'
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t ${IMAGE_NAME}:${BUILD_NUMBER} .'
                sh 'docker tag ${IMAGE_NAME}:${BUILD_NUMBER} ${IMAGE_NAME}:latest'
            }
        }

        stage('Deploy Container') {
            steps {
                sh '''
                    docker rm -f ${CONTAINER_NAME} || true
                    docker run -d \
                      --name ${CONTAINER_NAME} \
                      --restart unless-stopped \
                      -p ${HOST_PORT}:${CONTAINER_PORT} \
                      ${IMAGE_NAME}:latest
                '''
            }
        }
    }

    post {
        success {
            echo 'React application deployed successfully!'
        }

        failure {
            echo 'Pipeline failed. Check the console output.'
        }

        always {
            cleanWs()
        }
    }
}
