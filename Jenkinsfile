pipeline {
agent {
label {
label "QA"
}
}
tools {
  maven 'apache-maven-3.9.11'
}

stages {

stage ('one') {
steps {
sh """sudo cd /mnt/jenkins-slave/workspace/safsf/project
sudo mvn clean package
sudo cp /mnt/jenkins-slave/workspace/safsf/project/target/LoginWebApp.war /mnt/servers/apache-maven-11.0.13/webapps/ """
}
}


}
}
