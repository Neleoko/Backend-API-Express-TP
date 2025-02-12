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
        //stage('Build') {
           //steps {
                // TODO: Add build steps here
            //}
        //}
        stage('Test') {
            steps {
                sh 'npm install --save-dev mocha'
                sh 'npm run test'
            }
        }
    }
}
