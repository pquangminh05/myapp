pipeline {
    agent any
    tools {
        gradle 'Gradle'
        jdk 'JDK17'
    }
    environment {
        APP_NAME = 'myapp'
        ARTIFACT_PATH = 'build/libs/*.jar'
    }
    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/your-username/myapp-java.git', branch: 'main', credentialsId: 'github-credentials'
            }
        }
        stage('Build') {
            steps {
                sh 'gradle clean build -x test'
            }
        }
        stage('Test') {
            steps {
                sh 'gradle test'
            }
        }
        stage('Deploy') {
            steps {
                sh '''
                JAR_FILE=$(ls ${ARTIFACT_PATH} | head -1)
                pkill -f 'java -jar' || true
                nohup java -jar ${JAR_FILE} &
                sleep 5
                curl -f http://localhost:8080/hello || exit 1
                '''
            }
        }
    }
    post {
        always {
            archiveArtifacts artifacts: "${ARTIFACT_PATH}", allowEmptyArchive: true
        }
        success {
            echo 'CI/CD pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed!'
        }
    }
}
