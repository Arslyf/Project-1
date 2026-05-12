pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        stage('Build Image') {
            steps {
                sh 'docker build -t benim-uygulamam:latest .'
            }
        }
        stage('Deploy') {
            steps {
                // Önce çalışan eski bir konteyner varsa onu durdurup silelim ki port çakışmasın
                sh 'docker rm -f benim-app-konteyner || true'
                // Şimdi yeni imajı 8081 portundan ayağa kaldıralım (8080 Jenkins'e ait)
                sh 'docker run -d --name benim-app-konteyner -p 8081:80 benim-uygulamam:latest'
            }
        }
    }
}

