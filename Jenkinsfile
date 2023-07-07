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
        stage("deploy-dev"){
            steps{
                sshagent(['tomcat-new']) {
                sh """
                    scp -o StrictHostKeyChecking=no target/webapp.war  ec2-user@52.207.243.174:/home/ec2-user/apache-tomcat-10.1.10/webapps/
                    
                    ssh ec2-user@52.207.243.174 /home/ec2-user/apache-tomcat-10.1.10/bin/shutdown.sh
                    
                    ssh ec2-user@52.207.243.174 /home/ec2-user/apache-tomcat-10.1.10/bin/startup.sh
                
                """
            }
            
            }
        }
    }
}
