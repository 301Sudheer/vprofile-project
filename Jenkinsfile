pipeline {
    agent any
    tools {
        maven 'maven3'
    }
    environment {
        version = ''
    }
    stages {
        
        stage("Build Artifact") {
            steps {
                script {
                    sh 'mvn clean package -DskipTests'
                }
            }
        }
 stage('Deploy') {
        steps {
            sshagent(credentials: ['ubuntu']) {
                
                sh "ssh ubuntu@100.25.35.77 'sudo mv ~/vprofile-v1.war /var/lib/tomcat9/webapps/'"
                sh "ssh ubuntu@100.25.35.77 'sudo systemctl restart tomcat9'"
            }
        }
    }
    } // Closing stages block
} // Closing pipeline block
