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

        stage('Deploy by Docker-Compose') {
            steps {
                sh 'docker-compose -f docker-compose.yml up'
            }
        }
    }
}