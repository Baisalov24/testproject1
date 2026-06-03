pipeline {
    agent any

    stages {

        stage("clone") {
            steps {
                git credentialsId: "github-token-cred", url: "https://github.com/Baisalov24/testproject1.git", branch: 'main'
            }

        }
        stage ("Build image") {
            steps {
                sh 'docker build -t html-app:latest .'
            }
        }
        stage ("Deploy") {
            steps {
                sh '''
                docker stop html-app || true
                docker rm html-app || true

                docker run -d \\
                  --name html-app \\
                  -p 8081:80 \\
                  html-app:latest
                '''
            }
        }
    }
}