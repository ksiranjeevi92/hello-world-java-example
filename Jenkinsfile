def tag_val = 'v*.*.*-alpha'

pipeline {
    agent any
    environment {        
        NAME = 'Siranjeevi'
        TEAM = 'DX'
    }
    options{
        buildDiscarder(logRotator(daysToKeepStr: '1', numToKeepStr: '30', artifactNumToKeepStr: '30'))
    }
    stages {
        stage('Build') {
            when{
                tag tag_val
            }
            steps {
                bat 'echo "My first pipeline"'
                bat '''
                    echo "By the way, I can do more stuff in here"
                '''
                bat 'mvn clean package'
            }
        }
        stage ('Deploy') {
            when{
                beforeAgent true
                branch tag_val
            }
            steps {
                script {
                    deploy adapters: [tomcat8(credentialsId: 'tomcat-deployer', path: '', url: 'http://localhost:8080')],contextPath: '', onFailure: false, war: '**/*.war' 
                }
            }
        }      
    }
    post {
        always {
            bat 'echo I will always get executed :D'
        }
        success {
            bat 'echo I will only get executed if this success'
            archiveArtifacts artifacts: '**/*.war', fingerprint: true
        }
        failure {
            bat 'echo I will only get executed if this fails'
        }
        unstable {
            bat 'echo I will only get executed if this is unstable'
        }
    }
}