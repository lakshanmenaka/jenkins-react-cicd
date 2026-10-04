pipeline {
    agent any

    environment {
        // Docker image details
        IMAGE_NAME = 'react-cicd-app'
        CONTAINER_NAME = 'react-app-container'
        PORT = '80'
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', credentialsId: 'github-ssh-key-2', url: 'git@github.com:lakshanmenaka/jenkins-react-cicd.git'
            }
        }

        stage('Docker Build & Deploy') {
    steps {
        // 1. Docker image eka build kirima
        sh 'docker build -t react-cicd-app .'
        
        // 2. Parana container ekak run wenawanam eka stop karala remove kirima
        sh 'docker stop react-app-container || true'
        sh 'docker rm react-app-container || true'
        
        // 3. Aluth image eken container eka run kirima (Port 80)
        sh 'docker run -d -p 80:80 --name react-app-container react-cicd-app'
    }
}

        stage('Stop Existing Container') {
            steps {
                // Kalin run wena container ekak thiyenawanam eka nawatha remove kirima
                sh '''
                    docker stop ${CONTAINER_NAME} || true
                    docker rm ${CONTAINER_NAME} || true
                '''
            }
        }

        stage('Deploy Container') {
            steps {
                // Aluth image eken container eka run kirima
                sh "docker run -d -p ${PORT}:80 --name ${CONTAINER_NAME} ${IMAGE_NAME}:latest"
            }
        }
    }

    post {
        always {
            cleanWs()
        }
    }
}
