pipeline {
    agent any
    environment {        
        NAME = 'Siranjeevi'
        TEAM = 'DX'
    }
    stages {
        stage('Build') {
            steps {
                bat 'echo "My first pipeline"'
                bat '''
                    echo "By the way, I can do more stuff in here"
                    ls -lah
                '''
            }
        }
        stage ('Deploy') {
            steps {
                script {
                    deploy adapters: [tomcat7(credentialsId: 'tomcat-deployer', path: '', url: 'http://localhost:8080')], onFailure: false, war: '**/*.war' 
                }
            }
        }  
        stage ("Print My Name") {
            steps{
                script{
                    bat """"
                      echo Maintainer  ${env.NAME} frpm ${env.TEAM}
                    """"
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