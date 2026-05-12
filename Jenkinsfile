pipeline {
    agent any
    environment {
        DOCKER_HUB_USER = 'devarsyf'
    }
    stages {
        stage('Build & Tag') {
            steps {
                sh "docker build -t ${DOCKER_HUB_USER}/ilk-uygulamam:latest ."
            }
        }
        stage('Login & Push') {
            steps {
                // Jenkins'e tanıttığımız credential'ı güvenli şekilde çağırıyoruz
                withCredentials([usernamePassword(credentialsId: 'docker-hub-credentials', passwordVariable: 'DOCKER_HUB_PASSWORD', usernameVariable: 'DOCKER_HUB_USERNAME')]) {
                    sh "echo \$DOCKER_HUB_PASSWORD | docker login -u \$DOCKER_HUB_USERNAME --password-stdin"
                    sh "docker push ${DOCKER_HUB_USER}/ilk-uygulamam:latest"
                }
            }
        }
    }
}

