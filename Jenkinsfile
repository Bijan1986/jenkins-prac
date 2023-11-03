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
                script {
                            def jacocoPath = '**/target/jacoco.exec'
                            def jacocoReportPath = '**/target/site/jacoco'

                            publishCoverage adapters: [jacocoAdapter('**/target/jacoco.exec')], reportDir: '**/target/site/jacoco', reportFile: 'index.html'
                        }
            }
        }
    }
}