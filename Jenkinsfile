pipeline {
    agent any

    parameters {
        string(name: 'BRANCH_NAME', defaultValue: 'main', description: 'GitHub Branch')
        choice(name: 'ENVIRONMENT', choices: ['staging', 'production'], description: 'Deployment Environment')
    }

    stages {

        stage('Clone Repository') {
            steps {
                git branch: "${params.BRANCH_NAME}",
                url: 'https://github.com/Frogman46/cloudbox-app.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t cloudbox-app .'
            }
        }

        stage('Deploy Container') {
            steps {
                sh 'docker compose down || true'
                sh 'docker compose up -d'
            }
        }
    }
}
