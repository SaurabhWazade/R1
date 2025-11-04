pipeline {
agent {
label {
label "built-in"
}
}

stages {

stage ('one') {
steps {
sh """aws mb s3://kakaji789456123 --region ap-south-1

aws cp /root/project/target/LoginWebApp.war s3://kakaji789456123"""
}
}


}
}
