pipeline {
    agent {
        docker {
            image 'med3301/jenkins-agent:1.0'  // Docker image from Docker Hub
            reuseNode true  // Reuse the same node for multiple steps, reducing overhead
        }
    }

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
        
        // Additional stages (e.g., Build, Test) can go here
    }
}
