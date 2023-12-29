pipeline {
    agent { label 'Jenkins-Agent' }
    tools {
        // Update these with the names configured in Jenkins for Java and Maven
        jdk 'Name-Configured-in-Jenkins-for-Java17'
        maven 'Name-Configured-in-Jenkins-for-Maven3'	    
    }

    stages {
        stage("Cleanup Workspace") {
            steps {
                cleanWs()
            }
        }
        stage("Checkout from SCM") {
            steps {
                git branch: 'main', credentialsId: 'github', url: 'https://github.com/Sofoniasm/register-app'
            }
        }
        stage("Build Application") {
            steps {
                script {
                    sh "mvn clean package"
                }
            }
        }
        stage("Test Application") {
            steps {
                script {
                    sh "mvn test"
                }
            }
        }
        stage("SonarQube Analysis") {
            steps {
                script {
                    withSonarQubeEnv(credentialsId: 'Jenkins-Sonarqube-token') {
                        sh "mvn sonar:sonar"
                    }
                }
            }
        }
    }
}
