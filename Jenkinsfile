pipeline {

    agent none

    environment {
        PROJECT_URL     = "https://github.com/Shantanumajan6/project.git"
        COMPOSE_URL     = "https://github.com/SaurabhWazade/for-project-1.git"
        COMPOSE_DIR     = "for-project-1"

        DEV_IP          = "10.10.1.12"
        QA_IP           = "10.10.2.218"

        SHUTDOWN_DIR    = "for-project-1"
    }

    stages {

        /* -----------------------------------------------------------
           1) BUILD APPLICATION (BUILT-IN AGENT)
        ----------------------------------------------------------- */
        stage("Clone Project") {
            agent {
                label {
                    label "built-in"
                    customWorkspace "/mnt/projects"
                }
            }
            steps {
                sh "rm -rf *"
                sh "git clone ${PROJECT_URL}"
            }
        }

        stage("Build Project") {
            agent {
                label {
                    label "built-in"
                    customWorkspace "/mnt/projects"
                }
            }
            steps {
                sh "rm -rf /home/velocity/.m2"
                sh "cd project && mvn clean install -DskipTests=true"
            }
        }

        stage("Copy WAR to Shared Dir") {
            agent {
                label {
                    label "built-in"
                    customWorkspace "/mnt/projects"
                }
            }
            steps {
                sh "rm -rf /mnt/wars/*"
                sh "cp project/target/LoginWebApp.war /mnt/wars"
            }
        }


        /* -----------------------------------------------------------
           2) COPY WAR TO DEV & QA SERVERS
        ----------------------------------------------------------- */
        stage("Copy WAR to DEV") {
            agent {
                label {
                    label "built-in"
                    customWorkspace "/mnt/wars"
                }
            }
            steps {
                sh """scp LoginWebApp.war velocity@${DEV_IP}:/mnt/wars
                    unzip LoginWebApp.war
	     	    rm -rf LoginWebApp.war
		    sed -i 's|localhost|velocity|g' userRegistration.jsp
		    zip -r LoginWebApp.war * """

            }
        }

        stage("Copy WAR to QA") {
            agent {
                label {
                    label "built-in"
                    customWorkspace "/mnt/wars"
                }
            }
            steps {
                sh """scp LoginWebApp.war velocity@${QA_IP}:/mnt/wars
                      unzip LoginWebApp.war
	     	      rm -rf LoginWebApp.war
		      sed -i 's|localhost|velocity|g' userRegistration.jsp
		      zip -r LoginWebApp.war * """
            }
        }


        /* -----------------------------------------------------------
           3) DEV ENVIRONMENT DEPLOYMENT
        ----------------------------------------------------------- */
        stage("Clone Compose Repo (DEV)") {
            agent {
                label {
                    label "dev"
                    customWorkspace "/mnt/project"
                }
            }
            steps {
                sh "rm -rf *"
                sh "git clone ${COMPOSE_URL}"
            }
        }

        stage("Run Compose (DEV)") {
            agent {
                label {
                    label "dev"
                    customWorkspace "/mnt/project"
                }
            }
            steps {
                sh "cd ${COMPOSE_DIR} && sudo docker-compose up -d"
            }
        }


        /* -----------------------------------------------------------
           4) QA ENVIRONMENT DEPLOYMENT
        ----------------------------------------------------------- */
        stage("Clone Compose Repo (QA)") {
            agent {
                label {
                    label "qa"
                    customWorkspace "/mnt/project"
                }
            }
            steps {
                sh "rm -rf *"
                sh "git clone ${COMPOSE_URL}"
            }
        }

        stage("Run Compose (QA)") {
            agent {
                label {
                    label "qa"
                    customWorkspace "/mnt/project"
                }
            }
            steps {
                sh "cd ${COMPOSE_DIR} && sudo docker-compose up -d"
            }
        }
}
}
