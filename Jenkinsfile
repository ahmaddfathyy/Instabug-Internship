pipeline {
    agent any

    stages {
        stage('Docker Build') {
            steps {
                script {
                    docker.build('ahmaddfathyy/Go-Project:latest') {
                        sh 'docker build -t Go-App .'
                    }
                }
            }
        }
        stage('Docker Push') {
            steps {
                script {
                    docker.withRegistry('https://registry.hub.docker.com', 'Docker-Credentials') {
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
