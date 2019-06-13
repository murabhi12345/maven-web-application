node{

 def mvnhome = tool name: 'Maven 3.6.1', type: 'maven'

 stage('check out from Github')
    {    
        git credentialsId: 'bfdafd2f-c511-4076-b71a-9c064ab77c6c', url: 'https://github.com/murabhi12345/maven-web-application.git'
    }

 stage('Build the downloaded Code')
    {
        sh "${mvnhome}/bin/mvn clean package"
    }
    
 stage('Quality Code Check Using Sonar')
    {
        sh "${mvnhome}/bin/mvn sonar:sonar"
    } 
    
 stage('Upload Artifact to Nexus')
    {
        sh "${mvnhome}/bin/mvn deploy"
    } 
 stage('Deploy to TomCat')
   {
   
   sshagent(['TomCat']) 
   {
    sh "scp -o StrictHostKeyChecking=no  target/maven-web-application.war ec2-user@52.66.35.209:/opt/apache-tomcat-9.0.20/webapps/maven-web-application.war" 
   }
  
}
}
