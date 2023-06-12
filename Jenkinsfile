pipeline {
    agent any

    stages {
        stage('Docker Build') {
            steps {
                script {
                    docker.build('Go-Project:latest')
                }
            }
        }
        stage('Docker Push') {
            steps {
                script {
                    docker.withRegistry('https://registry.hub.docker.com', 'credentials-id') {
                        sh 'docker push ahmaddfathyy/Go-Project:latest'
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
