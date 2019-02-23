node('master') 
{
    stage('ContinuousDownload')
    {
       git 'https://github.com/thrinadhp/maven.git'
    }
    stage('ContinuousBuild')
    {
       sh 'mvn package'
    }
    stage('ContinuousDeployment')
    {
        sh 'scp /root/.jenkins/workspace/script/webapp/target/webapp.war ubuntu@172.31.20.70:/var/lib/tomcat7/webapps/qaenv.war'
    }
    stage('ContinuousTesting')
    {
        git 'https://github.com/selenium-saikrishna/TestingNew.git'
        sh 'java -jar /root/.jenkins/workspace/script/testing.jar'
    }
    stage('ContinuousDelivery')
    {
        input message: 'Waiting for approval from Delivery Manager!', submitter: 'kumar'
        sh 'scp /root/.jenkins/workspace/script/webapp/target/webapp.war ubuntu@:172.31.22.148/var/lib/tomcat7/webapps/prodenv.war'
    }
    
  
}
