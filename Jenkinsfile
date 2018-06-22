pipeline {
    agent any

tools {
        maven 'localMAVEN'
}
    parameters {
         string(name: 'staging', defaultValue: '18.208.129.98', description: 'Staging Server')
         string(name: 'deploying', defaultValue: '54.175.181.70', description: 'Production Server')
    }

    triggers {
         pollSCM('* * * * *')
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

        stage ('Deployments'){
            parallel{
                stage ('Deploy to Staging'){
                    steps {
                        bat "scp -i F:/LATEST JENKINS/bitnami/tomcatbybitnami.pem **/target/*.war ubuntu@ec2${params.staging}:/opt/bitnami/apache-tomcat/webapps"
                    }
                }

                stage ("Deploy to Production"){
                    steps {
                        bat "scp -i F:/LATEST JENKINS/bitnami/tomcatbybitnami2.pem **/target/*.war ubuntu@ec2${params.deploying}:/opt/bitnami/apache-tomcat/webapps"
                    }
                }
            }
        }
    }
}
