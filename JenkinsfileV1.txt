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

        stage('Build Images') {
            steps {
                sh 'docker build -t pzalove24/dashboard-application:client-latest client'
                sh 'docker build -t pzalove24/dashboard-application:server-latest server'
                sh 'docker build -t pzalove24/dashboard-application:nginx-latest nginx'
            }
        }

        // stage('Push Images to DockerHub') {
        //     steps {
        //         withCredentials([usernamePassword(credentialsId: 'dockerhub', passwordVariable: 'DOCKER_PASSWORD', usernameVariable: 'DOCKER_USERNAME')]) {
        //             sh 'docker login -u $DOCKER_USERNAME -p $DOCKER_PASSWORD'
        //             sh 'docker push pzalove24/Dashboard-Application:client-latest'
        //             sh 'docker push pzalove24/Dashboard-Application:server-latest'
        //             sh 'docker push pzalove24/Dashboard-Application:nginx-latest'
        //         }
        //     }
        // }
        // stage('Deploy by Docker-Compose') {
        //     steps {
        //         sh 'docker-compose -f docker-compose.yml up'
        //     }
        // }
    }
}