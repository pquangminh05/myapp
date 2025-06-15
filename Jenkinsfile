pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                // Lấy code từ GitHub
                checkout scm
            }
        }

        stage('Build') {
            steps {
                // Chạy build bằng wrapper có sẵn trong repo
                sh './gradlew build'
            }
        }

        stage('Test') {
            steps {
                sh './gradlew test'
            }
        }

        stage('Archive') {
            steps {
                // Lưu artifact nếu có file .jar hoặc build output
                archiveArtifacts artifacts: '**/build/libs/*.jar', fingerprint: true
            }
        }
    }
}
