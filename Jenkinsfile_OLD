pipeline {
    agent any

    tools {
        jdk 'JAVA_HOME'
        maven 'M2_HOME'
    }

    stages {

        stage("checkout") {
            steps {
                git 'https://github.com/satapathytanmay/webapp.git'
            }
        }

        stage("compile") {
            steps {
                sh 'mvn compile'
            }
        }

        stage("test") {
            steps {
                sh 'mvn test'
            }
        }

        stage("package") {
            steps {
                sh 'mvn clean package'
                sh 'mv target/*.war target/myweb.war'
            }
        }

        stage("deploy") {
            steps {
                sh '''
                cp target/myweb.war /home/ec2-user/tomcat10/webapps/

                /home/ec2-user/tomcat10/bin/shutdown.sh
                sleep 5
                /home/ec2-user/tomcat10/bin/startup.sh
                '''
            }
        }
    }
}
