pipeline {
    agent any

    stages {
        stage('Docker Build') {
            steps {
                sh 'docker build . -t go-project'
            }
        }
        stage('Push Image') {
            steps {
                script {
                    docker.withRegistry('https://index.docker.io/v1/', 'Docker-Credentials') {
                    def image = docker.build("ahmaddfathyy/go-app:latest")
                    image.push()
                    }
                }
            }
        }
    }

    // post {
    //     always {
    //         cleanWs()
    //         docker.image('ahmaddfathyy/Go-Project:latest').withRun { c ->
    //             sh "docker rmi ${c.id}"
    //         }
    //     }
    // }
}