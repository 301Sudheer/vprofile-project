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
    } // Closing stages block
} // Closing pipeline block
