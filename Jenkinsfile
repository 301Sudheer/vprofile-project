pipeline {
    agent any
    tools {
        maven 'maven3'
    }
    environment {
        version = '1.0.0' // Set your version here
    }
    stages {
        stage("Build Artifact") {
            steps {
                script {
                    def mvnCmd = 'mvn clean package -DskipTests'
                    def mvnOutput = sh(script: mvnCmd, returnStdout: true).trim()
                    echo "Maven Output: ${mvnOutput}"
                }
            }
        }
        stage('Deploy') {
            steps {
                script {
                    try {
                        sshagent(credentials: ['ubuntu']) {
                            def remoteCommands = [
                                "sudo mv ~/vprofile-v1.war /var/lib/tomcat9/webapps/",
                                "sudo systemctl restart tomcat9"
                            ]
                            remoteCommands.each { command ->
                                sh "ssh ubuntu@100.25.35.77 '${command}'"
                            }
                        }
                    } catch (Exception e) {
                        echo "Deployment failed: ${e.message}"
                        currentBuild.result = 'FAILURE'
                        throw e
                    }
                }
            }
        }
    } // Closing stages block
} // Closing pipeline block


