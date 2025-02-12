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
                script {
                    docker.withRegistry('https://registry.hub.docker.com', 'docker-hub') {
                    docker.image('neleoko/backend-api').push('latest')
                    }
                }
            }
        }
    }
}
