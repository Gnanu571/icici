node{
def mavenhome = tool name: "maven"
  properties([buildDiscarder(logRotator(artifactDaysToKeepStr: '', artifactNumToKeepStr: '', daysToKeepStr: '', numToKeepStr: '5'))])
stage ('git'){
git branch: 'development', credentialsId: 'a88f937b-a405-4e0a-8287-7968fa29801e', url: 'https://github.com/Gnanu571/icici.git'
}
stage ('build'){
sh "${mavenhome}/bin/mvn clean package"
}
stage ('sonarqube'){
sh "${mavenhome}/bin/mvn clean sonar:sonar"
}
stage ('nexus'){
sh "${mavenhome}/bin/mvn clean deploy"
}
stage('tomcat'){
sshagent(['059e424a-0489-49d8-9f02-80b595aba86e']) {
sh "scp -o StrictHostkeychecking=no target/maven-web-application.war ec2-user@35.89.6.162:/opt/apache-tomcat-9.0.83/webapps/"
}
}
}//node end
