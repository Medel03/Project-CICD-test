pipeline {
    agent {
        docker {
            image 'med3301/jenkins-agent:1.0'  // Replace with your actual Docker image name
            reuseNode true  // Optionally reuse the same node for multiple steps
        }
    }
    tools {
        jdk 'Java17'
        maven 'Maven3'
    }

    stages {
        stage("Cleanup Workspace") {
            steps {
                cleanWs()
            }
        }

        stage("Checkout from SCM") {
            steps {
                git branch: 'main', credentialsId: 'github', url: 'https://github.com/Medel03/Project-CICD-test'
            }
        }
        
    }
}
