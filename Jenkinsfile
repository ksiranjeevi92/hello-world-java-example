pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                bat 'mvn clean package'
            }
        }
        stage('Test') {
            steps {
                bat 'mvn test'
            }
        }
        stage('Deploy') {
            when { tag "release-*" }
            steps {
                bat 'echo make deploy'
            }
        }
    }
    post{
        always{
            cleanWs()
        }
    }
}