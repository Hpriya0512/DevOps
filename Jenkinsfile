pipeline {
    agent any

    stages {
        stage('Git Checkout') {
            steps {
                git branch: 'main', credentialsId: 'Devops', url: 'https://github.com/Hpriya0512/DevOps'
            }
        }
        stage('Maven Build') {
            steps {
                sh 'mvn clean package'
            }
        }
        stage('Tomcat Deploy - Dev') {
            steps {
                sshagent(['tomcat-dev']) {
                    sh "scp -o StrictHostKeyChecking=no target/hr-api.war ec2-user@172.31.84.30:/opt/tomcat9/webapps/"
                    sh "ssh ec2-user@172.31.84.30 /opt/tomcat9/bin/shutdown.sh"
                    sh "ssh ec2-user@172.31.84.30 /opt/tomcat9/bin/startup.sh"
                }
            }
        }
    }
}
