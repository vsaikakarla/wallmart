node
{

def mavenHome = tool name: "maven3.6.3"

stage('CheckoutCode')
{
git branch: 'development', credentialsId: '9c1d758d-3d4f-47f7-a564-90f0a0d434ab', url: 'https://github.com/vsaikakarla/wallmart.git'
}
stage('Build')
{
sh "${mavenHome}/bin/mvn clean package"
}

stage('ExecuteSonarQubeReport')
{
sh "${mavenHome}/bin/mvn sonar:sonar"
}
stage('Upload Artifactsinto Nexus')
{
sh "${mavenHome}/bin/mvn deploy"
}
stage('DeployAppIntoTomcatServer')
{
  sshagent(['5c951448-2dbc-4399-871d-7d871c6805c9']) {
  sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war ec2-user@172.31.93.245:/opt/tomcat9/webapps/"
  }
}
}
