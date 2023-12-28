pipeline{
    agent any
    stages{
        stage("code checkout"){
            steps{
             git branch: 'main', credentialsId: 'github', url: 'https://github.com/Maddujagadeesh/way2news-online.git'   
                
            }
        }
         stage("maven build"){
            steps{
             sh 'mvn package'
                
            }
        }
        stage("Dev deploy"){
            steps{
            sshagent(['tomcat-dev']) {
            //copy war file to tomcat dev server
             sh"scp -o StrictHostKeyChecking=no target/way2news-online.war ec2-user@172.31.18.167:/opt/tomcat9/webapps/"
             //Restart tomcat server
             sh"ssh ec2-user@172.31.18.167 /opt/tomcat9/bin/shutdown.sh"
             sh"ssh ec2-user@172.31.18.167 /opt/tomcat9/bin/startup.sh"
               }
                
            }
        }
    }
}
