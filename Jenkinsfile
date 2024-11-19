pipeline {
    agent {
        docker {
            image 'med3301/jenkins-agent:1.0'
            args '--user root -v /var/run/docker.sock:/var/run/docker.sock' // mount Docker socket to access the host's Docker daemon
            args '--user root -v /var/lib/jenkins/workspace/e2e-pipeline-test:/var/lib/jenkins/workspace/e2e-pipeline-test'

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
