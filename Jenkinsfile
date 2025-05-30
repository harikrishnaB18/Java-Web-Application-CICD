pipeline {
    agent any

    tools {
        maven 'Maven3'    // Maven tool name as configured in Jenkins
        jdk 'JDK11'       // JDK configured in Jenkins
    }

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/harikrishnaB18/Java-Web-Application-CICD.git'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Deploy') {
            steps {
                sshagent(['tomcat-ec2-key']) {
                    sh """
                    scp target/my-java-webapp.war ubuntu@15.207.221.227:/opt/tomcat9/webapps/
                    ssh ubuntu@15.207.221.227 '/opt/tomcat9/bin/shutdown.sh || true && /opt/tomcat9/bin/startup.sh'
                    """
                }
            }
        }
    }
}
