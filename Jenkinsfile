pipeline {
    agent any
    tools {
        maven 'localMAVEN'
    }
       stages{
        stage('Build'){
            steps {
              bat 'call mvn clean package'            
            }
            post {
                success {
                    echo 'Now Archiving...'
                    archiveArtifacts artifacts: '**/target/*.war'
                }
            }
        }
        stage('deployments'){
            steps {
                Build job: 'deploy-to-staging'
                Build job: 'deploy-to-prod'
            }
            }

        }
    }

