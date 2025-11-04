pipeline {
agent {
label {
label "QA"
}
}

stages {

stage ('one') {
steps {
sh """sudo git clone https://github.com/SaurabhWazade/project.git
  sudo cd /root/project/
  sudo mvn clean package
  sudo cp /root/project/target/LoginWebApp.war /mnt/servers/apache-maven-11.0.13/webapps/ """
}
}


}
}
