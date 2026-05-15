pipeline {
    agent any

    tools {
        maven 'Maven 3.9'
    }

    stages {

        stage('Checkout') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/Sid197/git-journey.git'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean package -DskipTests'
            }
        }

        stage('Test') {
            steps {
                sh 'mvn test'
            }
            post {
                always {
                    junit '**/target/surefire-reports/*.xml'
                }
            }
        }

        stage('Archive') {
            steps {
                archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
            }
        }

        stage('Deploy') {
            steps {
                echo "✅ Build #${BUILD_NUMBER} complete — JAR is ready!"
            }
        }
    }

    post {
        success { echo "✅ Build #${BUILD_NUMBER} succeeded!" }
        failure  { echo "❌ Build #${BUILD_NUMBER} failed!" }
    }
}
