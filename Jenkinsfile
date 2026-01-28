pipeline {
    agent any

    tools {
        nodejs 'node18'
    }

    stages {

        stage('Clone Repository') {
            steps {
                git branch: 'main', url: 'https://github.com/<your-username>/react-cicd-app.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }

        stage('Run Tests') {
            steps {
                sh 'npm test -- --watchAll=false'
            }
        }

        stage('Build React App') {
            steps {
                sh 'npm run build'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t react-cicd-app:latest .'
            }
        }

        stage('Deploy to Docker Swarm') {
            steps {
                sh '''
                docker service update --force react_app || \
                docker service create --name react_app -p 80:80 react-cicd-app:latest
                '''
            }
        }
    }
}
