pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build') {
            steps {
                bat 'gradlew.bat build'
            }
        }

        stage('Test') {
            steps {
                bat 'gradlew.bat test'
            }
        }

        stage('Archive') {
            steps {
                archiveArtifacts artifacts: '**/build/libs/*.jar', fingerprint: true
            }
        }

        stage('Deploy') {
            steps {
                bat 'java -jar build\\libs\\your-app-name-0.0.1-SNAPSHOT.jar'
            }
        }
    }
}

