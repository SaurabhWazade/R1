pipeline {
    agent { label 'QA' }

    tools {
        maven 'apache-maven-3.9.11'
    }

    stages {
        stage('Clone Repository') {
            steps {
                sh '''
                    git clone https://github.com/SaurabhWazade/project.git
                '''
            }
        }

        stage('Build with Maven') {
            steps {
                dir('project') {
                    sh '''
                        mvn clean package
                    '''
                }
            }
        }

        stage('Deploy WAR') {
            steps {
                sh '''
                    sudo cp project/target/LoginWebApp.war /mnt/servers/apache-tomcat-10.1.48/webapps/
                '''
            }
        }
    }
}

