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
    } // Closing stages block
} // Closing pipeline block
