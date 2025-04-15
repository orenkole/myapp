pipeline {
    agent any

    environment {
        DOCKER_CREDENTIALS_ID = 'dockerhubkey'
        DOCKER_IMAGE = 'orenkole/myapp'
    }

    stages {
        stage('Clone the repository') {
            steps {
                git branch: 'main', url: 'https://github.com/orenkole/myapp.git'
            }
        }
        stage('Build docker image') {
            steps {
                script {
                    docker.build(DOCKER_IMAGE)
                }
            }
        }
        stage('Run tests') {
            steps {
                script {
                    sh "echo 'run some tests'"
                }
            }
        }
        stage('Push to the docker registry') {
            steps {
                script {
                    docker.withRegistry('https://index.docker.io/v1/', DOCKER_CREDENTIALS_ID) {
                        docker.image(DOCKER_IMAGE).push()
                    }
                }
            }
        }
    }
}