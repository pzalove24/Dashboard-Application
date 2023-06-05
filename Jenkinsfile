pipeline {
    agent any

    environment {
        MONGO_URL = credentials('mongodb-uri')
        PORT = credentials('port')
        REACT_APP_BASE_URL = credentials('react-app-base-url')
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Client Tests') {
            steps {
                dir('client') {
                    sh 'npm install'
                }
            }
        }
        // stage('Server Tests') {
        //     steps {
        //         dir('server') {
        //             sh 'npm install'
        //             sh 'export MONGO_URL=$MONGO_URL'
        //             sh 'export PORT=$PORT'
        //             sh 'export REACT_APP_BASE_URL=$REACT_APP_BASE_URL'
        //         }
        //     }
        // }
        // stage('Build Images') {
        //     steps {
        //         sh 'docker build -t pzalove24/My-Dashboard-Template:client-latest client'
        //         sh 'docker build -t pzalove24/My-Dashboard-Template:server-latest server'
        //     }
        // }
        // stage('Push Images to DockerHub') {
        //     steps {
        //         withCredentials([usernamePassword(credentialsId: 'dockerhub', passwordVariable: 'DOCKER_PASSWORD', usernameVariable: 'DOCKER_USERNAME')]) {
        //             sh 'docker login -u $DOCKER_USERNAME -p $DOCKER_PASSWORD'
        //             sh 'docker push rakeshpotnuru/productivity-app:client-latest'
        //             sh 'docker push rakeshpotnuru/productivity-app:server-latest'
        //         }
        //     }
        // }
    }
    
}