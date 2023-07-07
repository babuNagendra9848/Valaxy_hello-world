pipeline{
    agent any
    
   environment{
     PATH = "/opt/maven3/bin:$PATH"
    }
    stages{
        stage("Git Checkout"){
            steps{
           git credentialsId: 'GurusGhub', url: 'https://github.com/GurusGhub/Valaxy_hello-world.git'
            }
        }
        stage("Maven Build"){
            steps{
                sh "mvn clean install"
              
            }
        }
      stage("Deploy to tomcat"){
            steps{
                sshagent(['Deploy_user']) {
               sh """
               scp -o StrictHostKeyChecking=no webapp/target/webapp.war ec2-user@172.31.87.199:/opt/tomcat/webapps"
               ssh ec2-user@172.31.87.199 /opt/tomcat/bin/shutdown.sh
               ssh ec2-user@172.31.87.199 /opt/tomcat/bin/startup.sh
               """
               }
            }
        }     
    }
}
