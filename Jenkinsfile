pipeline {
    agent {
        docker {
            image 'med3301/jenkins-agent:1.1'
            args '--user root -v /var/run/docker.sock:/var/run/docker.sock -v /var/lib/jenkins/workspace:/workspace' // mount Docker socket to access the host's Docker daemon
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

        stage("Build Application") {
            steps {
                sh 'ls -ltr /workspace''
                sh 'cd /workspace && mvn clean package'
            }
        }

        stage("Test Application") {
            steps {
                sh 'cd /workspace && mvn test'
            }
        }
        
    }
}
