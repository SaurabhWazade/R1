pipeline {
    agent { label 'QA' }

    tools {
        maven 'apache-maven-3.9.11'
    }

    stages {

        stage('Deploy WAR') {
            steps {
                sh '''
                    sudo cp project/target/LoginWebApp.war /mnt/servers/apache-tomcat-10.1.48/webapps/
                '''
            }
        }
    }
}

