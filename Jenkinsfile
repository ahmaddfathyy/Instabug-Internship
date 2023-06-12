pipeline {
    agent any

    stages {
        stage('Docker Build') {
            steps {
                sh 'docker build . -t go-project:latest'
            }
        }
        stage('Push Image') {
            steps {
                script {
                    docker.withRegistry('https://index.docker.io/v1/', 'Docker-Credentials') {
                    def image = docker.build("ahmaddfathyy/go-project:latest")
                    image.push()
                    }
                }
            }
        }
    }

    post {
        always {
            cleanWs()
            docker.image('ahmaddfathyy/Go-Project:latest').withRun { c ->
                sh "docker rmi ${c.id}"
            }
        }
    }
}