pipeline {
    agent any

    environment {
        DOCKER_CREDENTIALS = 'dockerhub'
    }

    stages {
        stage('Clone repository') {
            steps {
                checkout scm
            }
        }

        stage('Build image') {
            steps {
                script {
                    app = docker.build("alenjangelov9720/kiii-jenkins")
                }
            }
        }

        stage('Push image') {
            when {
                expression { env.BRANCH_NAME == 'dev' }
            }
            steps {
                script {
                    docker.withRegistry('https://registry.hub.docker.com', DOCKER_CREDENTIALS) {
                        app.push("${env.BRANCH_NAME}-${env.BUILD_NUMBER}")
                        app.push("${env.BRANCH_NAME}-latest")
                        // signal the orchestrator that there is a new version
                    }
                }
            }
        }
    }
}
