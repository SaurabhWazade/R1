pipeline {
    agent { label 'QA' }

    tools {
        maven 'apache-maven-3.9.11'
    }

    stages {
        stage('Clone Repository') {
            steps {
                sh '''
                    rm -rf project
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
                    sudo cp project/target/LoginWebApp.war /mnt/servers/apache-tomcat-11.0.13/webapps/
                '''
            }
        }
    }
}

