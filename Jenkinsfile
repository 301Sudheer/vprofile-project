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
        stage("Test") {
            steps {
                script {
                    sh 'mvn test'
                }
            }
        }
        stage("Upload Artifact s3") {
            steps {
                script {
                    sh "mvn help:evaluate -Dexpression=project.version -q -DforceStdout > version.txt"
                    version = readFile('version.txt').trim()
                    sh "aws s3 cp target/vprofile-${version}.war s3://vprofile-artifacts1/vprofile-${version}.war"
                }
            }
        }
        stage('Deploy') {
            steps {
                sshagent(credentials: ['ubuntu']) {
                    sh "ssh ubuntu@3.110.159.232 'sudo mv ~/vprofile-${version}.war /var/lib/tomcat9/webapps/'"
                    sh "ssh ubuntu@3.110.159.232 'sudo systemctl restart tomcat9'"
                }
            }
        }
    }
}
