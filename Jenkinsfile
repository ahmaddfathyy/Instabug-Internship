pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
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