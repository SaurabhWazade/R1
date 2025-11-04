pipeline {
agent {
label {
label "built-in"
}
}

stages {

stage ('one') {
steps {
sh """scp -i "hey.pem" /root/project/target/LoginWebApp.war ec2-user@172.31.1.146:/mnt/servers/apache-tomcat-11.0.13/webapps/"""
}
}


}
}
