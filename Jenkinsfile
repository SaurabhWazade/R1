pipeline {

    agent none
     tools {
        maven "apache-maven-3.9.11"
    }


    environment {
        PROJECT_URL = "https://github.com/Shantanumajan6/project.git"
        COMPOSE_URL = "https://github.com/SaurabhWazade/for-project-1.git"
        COMPOSE_DIR = "for-project-1"

        DEV_IP      = "10.10.1.126"
        QA_IP       = "10.10.2.182"
    }

    stages {

        /* ---------- 1) BUILD APP ---------- */
        stage("Clone Project") {
            agent { label "built-in" }
            steps {
                sh "rm -rf *"
                sh "git clone ${PROJECT_URL}"
            }
        }

        stage("Build Project") {
            agent { label "built-in" }
            steps {
                sh "rm -rf /home/velocity/.m2"
                sh """
                    cd project
                    mvn clean install -DskipTests=true
                """
            }
        }

        /* ---------- 2) PREPARE WAR ---------- */
        stage("Prepare WAR") {
            agent { label "built-in" }
            steps {
                sh """
                    rm -rf /mnt/wars/*
                    cp project/target/LoginWebApp.war /mnt/wars

                    cd /mnt/wars
                    unzip LoginWebApp.war
                    rm LoginWebApp.war

                    sed -i 's|localhost|velocity|g' userRegistration.jsp

                    zip -r LoginWebApp.war *
                """
            }
        }

        /* ---------- 3) COPY WAR ---------- */
        stage("Copy WAR to DEV") {
            agent { label "built-in" }
            steps {
                sh "scp /mnt/wars/LoginWebApp.war velocity@${DEV_IP}:/mnt/wars"
            }
        }

        stage("Copy WAR to QA") {
            agent { label "built-in" }
            steps {
                sh "scp /mnt/wars/LoginWebApp.war velocity@${QA_IP}:/mnt/wars"
            }
        }

        /* ---------- 4) DEPLOY DEV ---------- */
        stage("Clone Compose Repo (DEV)") {
            agent { label "dev" }
            steps {
                sh "rm -rf *"
                sh "git clone ${COMPOSE_URL}"
            }
        }

        stage("Run Compose (DEV)") {
            agent { label "dev" }
            steps {
                sh "cd ${COMPOSE_DIR} && docker-compose up -d"
            }
        }

        /* ---------- 5) DEPLOY QA ---------- */
        stage("Clone Compose Repo (QA)") {
            agent { label "qa" }
            steps {
                sh "rm -rf *"
                sh "git clone ${COMPOSE_URL}"
            }
        }

        stage("Run Compose (QA)") {
            agent { label "qa" }
            steps {
                sh "cd ${COMPOSE_DIR} && docker-compose up -d"
            }
        }
    }
}
