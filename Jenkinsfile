pipeline {
    agent any

    tools {
        maven "maven_3_9_5"
    }

    environment {
        DOCKERHUB_CREDENTIALS = credentials('DockerHubCred2')
    }

    stages {
        stage('Build Maven') {
            steps {
                checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/Bijan1986/jenkins-prac']])
                sh 'mvn clean install'
            }
        }

        stage('Code Coverage') {
            steps {
                sh "./mvnw jacoco:report"
                publishHTML(target: [
                    reportDir: 'target/site/jacoco',
                    reportFiles: 'index.html',
                    reportName: "JaCoCo Report"
                ])
                sh "./mvnw jacoco:check"
            }
        }

        stage('Check Docker') {
            steps {
                sh '/usr/local/bin/docker --version'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    withCredentials([usernamePassword(credentialsId: 'DockerHubCred2', usernameVariable: 'DOCKERHUB_USERNAME', passwordVariable: 'DOCKERHUB_PASSWORD')]) {
                        sh "/usr/local/bin/docker login -u $DOCKERHUB_USERNAME -p $DOCKERHUB_PASSWORD"
                        sh '/usr/local/bin/docker build -t bijan1986/devops-integration .'
                        sh '/usr/local/bin/docker push bijan1986/devops-integration'
                    }
                }
            }
        }
    }
}
