pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', credentialsId: 'github-ssh-key-2', url: 'git@github.com:lakshanmenaka/jenkins-react-cicd.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }

        stage('Build React App') {
            steps {
                sh 'npm run build'
            }
        }

        stage('Test') {
            steps {
                sh 'CI=true npm test'
            }
        }
    }

    post {
        always {
            cleanWs()
        }
    }
}
