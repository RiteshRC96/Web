pipeline {
    agent any

    environment {
        MAVEN_HOME = 'C:/Program Files/Maven/apache-maven-3.9.9' // Windows path to Maven
    }

    tools {
        maven 'Maven 3.9.9'  // Ensure this matches your Jenkins Maven tool configuration
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/Gauri9977/My_webapp.git'
            }
        }
        
        stage('Build') {
            steps {
                // Run Maven build to clean and package the web app
                bat '"${MAVEN_HOME}/bin/mvn" clean package'
            }
        }

        stage('Test') {
            steps {
                // Run Maven test 
                bat '"${MAVEN_HOME}/bin/mvn" test'
            }
        }

        stage('Deploy to Tomcat') {
            steps {
                deploy adapters: [
                    tomcat9(credentialsId: 'tomcat-credentials', path: '', url: 'http://localhost:8080')
                ], war: '**/target/*.war'  // Ensure this path is correct
            }
        }
    }

    post {
        success {
            echo 'Deployment successful!'
        }
        failure {
            echo 'Deployment failed!'
        }
    }
}
