pipeline {
    agent {
        docker {
            image 'med3301/jenkins-agent:v2.0'
            args '--user root -v /var/run/docker.sock:/var/run/docker.sock -v /var/lib/jenkins/workspace:/var/lib/jenkins/workspace'
            
        } 
    }

    stages {
        stage('Check and Fix Permissions') {
            steps {
                script {
                    sh 'sudo chown -R jenkins:jenkins /var/lib/jenkins/workspace/e2e-pipeline-test/'
                    sh 'sudo chmod -R 755 /var/lib/jenkins/workspace/e2e-pipeline-test/target'

                    echo "Confirming permissions after fixing"
                    sh 'ls -lR /var/lib/jenkins/workspace/e2e-pipeline-test/target'
                }
            }
        }

        
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
        
        stage('Verify Workspace') {
            steps {
                script {
                    // Print current workspace directory
                    sh 'echo "Current Workspace: $(pwd)"'
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

        stage("Sonarqube Analysis") {
            steps {
                script {
                    withSonarQubeEnv(credentialsId: 'jenkins-sonar-token'){
                        sh "mvn sonar:sonar"
                    }
                }
            }
        }

         stage("Quality Gate") {
            steps {
                script {
                    waitForQualityGate abortPipeline: false, credentialsId: 'jenkins-sonar-token'
                }
            }
        }




        
        
    }
}
