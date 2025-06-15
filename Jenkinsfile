pipeline {
    agent any

    tools {
        gradle 'Gradle_7' // Cấu hình trong Jenkins trước (hoặc xóa nếu không có)
    }

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/pquangminh05/myapp.git'
            }
        }

        stage('Build') {
            steps {
                
                 bat './gradlew.bat build' 
            }
        }

        stage('Test') {
            steps {
                sh './gradlew test'
            }
        }
    }

    post {
        always {
            echo 'Done!'
        }
    }
}
