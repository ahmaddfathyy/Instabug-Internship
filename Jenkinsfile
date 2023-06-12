pipeline {
    agent any

    stages {
        stage('Docker Build') {
            steps {
                sh 'docker build . -t go-project'
            }
        }
        stage('Docker Push') {
            steps {
                script {
                    docker.withRegistry('https://registry.hub.docker.com', 'Docker-Credentials') {
                        sh 'docker push ahmaddfathyy/go-project:latest'
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