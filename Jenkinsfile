pipeline {
    agent any

    tools {
        jdk 'Java17'  // Ensure Java 17 is installed in your Docker container or your Jenkins environment
        maven 'Maven3'  // Ensure Maven 3 is installed in your Docker container or Jenkins environment
    }

    stages {
        stage("Cleanup Workspace") {
            steps {
                cleanWs()  // Clean the workspace before starting the build
            }
        }

        stage("Checkout from SCM") {
            steps {
                git branch: 'main', credentialsId: 'github', url: 'https://github.com/Medel03/Project-CICD-test'
            }
        }

        stage("Build Application and Test") {
            steps {
                sh 'ls -ltr'
                sh 'mvn clean package'
            }
        }

        stage("Test Application") {
            steps {
                sh 'mvn test'
            }
        }
        
    }
}
