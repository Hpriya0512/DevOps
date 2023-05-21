pipeline {
    agent any

    stages {
        stage('Git Checkout') {
            steps {
            git branch: 'main', credentialsId: 'd71cba70-7f21-4a56-b3f4-f94d366f05f0', url: 'https://github.com/Hpriya0512/DevOps'
            }
        }
        stage('Maven Build') {
            steps {
                sh 'mvn clean package'
            }
        }
        stage('Tomcat Deploy - Dev') {
            steps {
                sshagent(['Tomcat-dev']) {
    sh "scp -o StrictHostKeyChecking=no target/hr-api.war ec2-user@172.31.84.30:/opt/tomcat9/webapps/"
    sh "ssh ec2-user@172.31.84.30 /opt/tomcat9/bin/shutdown.sh"
    sh "ssh ec2-user@172.31.84.30 /opt/tomcat9/bin/shutdown.sh"
}
            }
        }
    }
}
