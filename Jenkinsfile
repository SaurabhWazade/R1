pipeline {
agent {
label {
label "QA"
}
}

stages {

stage ('one') {
steps {
sh """sudo git clone 
  sudo cp /root/.jenkins/workspace/safsf/project/target/LoginWebApp.war /mnt/servers/apache-maven-11.0.13/webapps/ """
}
}


}
}
