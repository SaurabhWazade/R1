pipeline {
agent {
label {
label "QA"
}
}

stages {

stage ('one') {
steps {
sh """aws cp s3://kakaji789456123/LoginWebApp.war /mnt/servers/apache-tomcat-11.0.13/webapps/"""
}
}


}
}
