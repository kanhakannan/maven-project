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
        stage('deploy to staging'){
            steps {
                build 'deploy-to-staging'
            }
        }
            stage('deploy to prod'){
            steps {
                timeout(time:5, unit:'DAYS'){
                    input message:'Approve PRODUCTION Deployment?'
                }
                build 'deploy-to-prod'
            }
        post {
                success {
                    echo 'Code deployed to Production.'
                }

                failure {
                    echo ' Deployment failed.'
                }
            }
        }


    }
}