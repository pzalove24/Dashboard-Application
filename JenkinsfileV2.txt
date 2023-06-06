pipeline {
    agent any

    environment {
        MONGO_URL = credentials('mongo_url')
        PORT = credentials('port')
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Credential Export') {
            steps {
                sh 'export MONGO_URL=$MONGO_URL'
                sh 'export PORT=$PORT'
            }
        }

        stage('Integration') {
            steps {
                sh 'docker-compose stop'
                sh 'docker-compose rm -f'
            }
        }

        stage('Deployment by Docker-Compose') {
            steps {
                sh 'docker-compose -f docker-compose.yml up'
            }
        }
    }
}