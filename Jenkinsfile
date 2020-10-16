node
 {
  
  def mavenHome = tool name: "maven3.6.3"
  
      echo "GitHub BranhName ${env.BRANCH_NAME}"
      echo "Jenkins Job Number ${env.BUILD_NUMBER}"
      echo "Jenkins Node Name ${env.NODE_NAME}"
  
      echo "Jenkins Home ${env.JENKINS_HOME}"
      echo "Jenkins URL ${env.JENKINS_URL}"
      echo "JOB Name ${env.JOB_NAME}"
  
   properties([[$class: 'JiraProjectProperty'], buildDiscarder(logRotator(artifactDaysToKeepStr: '', artifactNumToKeepStr: '2', daysToKeepStr: '', numToKeepStr: '2')), pipelineTriggers([pollSCM('* * * * *')])])
  
  stage("CheckOutCodeGit")
  {
   git branch: 'development', credentialsId: '65fb834f-a83b-4fe7-8e11-686245c47a65', url: 'https://github.com/MithunTechnologiesDevOps/maven-web-application.git'
 }
 node
{

def mavenhome = tool name : "maven-3.6.3"
properties([pipelineTriggers([pollSCM('* * * * *')])])

stage('checkout')
{
git branch: 'development', credentialsId: '90b0f2b9-015f-4c51-88c9-614a5c55490b', url: 'https://github.com/rahulbasha/maven-o-development.git'
}
stage('build')
{
sh"${mavenhome}/bin/mvn clean package"
}
stage('sonarqube report')
{
sh"${mavenhome}/bin/mvn sonar:sonar"
}
stage('tomcat')
{
sshagent(['04638fb0-2874-4771-bcbe-4fa755824044']) {
    sh "scp -o StrictHostKeychecking=no /var/lib/jenkins/workspace/maven-pipe/target/maven-web-application.war ec2-user@13.233.204.242://opt/apache-tomcat-8.5.57/webapps"
}
}
stage('email sent')
{
emailext body: '''build completed sucessfully!!

Thanks & regards,
Rahul basha shaik,
8074346494.''', subject: 'build succesfull!!!', to: 'rahulraees010@gmail.com'
}
}
