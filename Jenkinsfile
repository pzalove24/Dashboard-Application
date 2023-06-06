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

        stage('Remove Old Application') {
            steps {
                sh 'docker-compose kill'
                sh 'docker rmi -f peeratchai24/dashboard-server'
                sh 'docker rmi -f peeratchai24/dashboard-client'
                sh 'docker rmi -f peeratchai24/dashboard-nginx'
            }
        }

        stage('Deploy by Docker-Compose') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub', passwordVariable: 'DOCKER_PASSWORD', usernameVariable: 'DOCKER_USERNAME')]) {
                    sh 'docker login -u $DOCKER_USERNAME -p $DOCKER_PASSWORD'
                    sh 'docker-compose -f docker-compose.yml up'
                }
            }
        }
    }
}