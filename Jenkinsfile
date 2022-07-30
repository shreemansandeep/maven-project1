pipeline{
  agent any
  stages{
    stage("Git Checkout"){
      steps{
            git credentialsId: 'GitCred', url: 'https://github.com/shreemansandeep/maven-project1.git'
           }
          }
     stage("Maven Build"){
       steps{
            sh "mvn clean install package"
            sh "mv target/*.war target/myweb.war"
             }
            }
     stage("deploy-dev"){
       steps{
          sshagent(['tomcat-pipe']) {
          sh """
          scp -o StrictHostKeyChecking=no target/myweb.war  
          root@ip-172-31-35-79:/opt/tomcat/webapps/
          ssh root@ip-172-31-35-79 /opt/tomcat/bin/shutdown.sh
          ssh root@ip-172-31-35-79 /opt/tomcat/bin/startup.sh
           """
            }
          }
        }
      }
    }
