pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                checkout([
                    $class: 'GitSCM',
                    branches: [[name: '*/main']],
                    userRemoteConfigs: [[
                        url: 'https://github.com/Neleoko/Backend-API-Express-TP',
                        credentialsId: 'github-credentials'
                    ]]
                ])
            }
        }

        stage('Test') {
            steps {
                sh 'npm install --save-dev mocha'
                sh 'npm run test'
            }
        }

        stage('Build') {
            steps {
                sh 'docker build -t backend-api .'
            }
        }

        stage('Push') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'docker-hub', usernameVariable: 'DOCKER_USERNAME', passwordVariable: 'DOCKER_PASSWORD')]) {
                    sh 'echo "$DOCKER_PASSWORD" | docker login -u "$DOCKER_USERNAME" --password-stdin'
                    sh 'docker tag backend-api neleoko/backend-api:latest'
                    sh 'docker push neleoko/backend-api:latest'
                }
            }
        }
    }
}
