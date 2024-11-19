pipeline {
    agent {
        docker {
            image 'med3301/jenkins-agent:v2.0'
            args '--user root -v /var/run/docker.sock:/var/run/docker.sock' // mount Docker socket to access the host's Docker daemon
        } 
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

        stages {
        stage('Verify Workspace') {
            steps {
                script {
                    // Print current workspace directory
                    sh 'echo "Current Workspace: $(pwd)"'
                    }
                }
            }
        }

        stage("Build Application") {
            steps {
                sh "ls -ltr"
                sh "mvn clean package"
            }
        }

        stage("Test Application") {
            steps {
                sh "mvn test"
            }
        }
        
    }
}
