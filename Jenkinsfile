pipeline {
    agent any
    triggers {
         pollSCM('* * * * *')
    }
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
             sh "./mvnw jacoco:check"
                            sh "./mvnw jacoco:report"
                            publishHTML (target: [
                                           reportDir: 'target/site/jacoco',
                                           reportFiles: 'index.html',
                                           reportName: "JaCoCo Report"
                                      ])

            }
        }
    }
}