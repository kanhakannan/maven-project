pipeline {
    agent any
    tools {
        mvn 'localMAVEN'
    }
       stages{
        stage('Build'){
            steps {
              bat 'mvn clean package'
            }
            post {
                success {
                    echo 'Now Archiving...'
                    archiveArtifacts artifacts: '**/target/*.war'
                }
            }
        }
    }
}
