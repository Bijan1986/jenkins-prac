pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                // Checkout your source code here (e.g., Git)
                git branch: 'main', url: 'https://github.com/Bijan1986/jenkins-prac.git'
            }
        }
        stage('Build and Test using jenkinsfile') {
            steps {
                sh './mvnw clean package'
            }
        }
        stage('Code coverage'){
            steps{
                sh "./mvnw jacoco:test"
                sh "./mvnw jacoco:report"
                publishHTML (target: [
                               reportDir: 'build/reports/jacoco/test/html',
                               reportFiles: 'index.html',
                               reportName: "JaCoCo Report"
                          ])
            }
        }
    }
}