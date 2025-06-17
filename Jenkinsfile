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
        script {
            def jarFiles = findFiles(glob: 'build/libs/*.jar')
            if (jarFiles.length == 0) {
                error "No JAR file found to deploy"
            }
            def jarPath = jarFiles[0].path
            bat "java -jar ${jarPath}"
        }
    }
}
    }
}

