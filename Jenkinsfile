node {
    def mvnHome
    stage('Preparation') {
    steps {
        checkout([
            $class: 'GitSCM',
            branches: [[name: '*/main']],
            userRemoteConfigs: [[
                url: 'https://github.com/Neleoko/Backend-API-Express-TP',
                credentialsId:'github-credentials'
                ]]
                ])
                }
    }
}
