#!groovy
pipeline {
    environment {
        DEMO = "Demo"
    }
    
    agent {
        docker {
            image "ssriram12/maven-3.9.9:jdk13"
            label "docker"
            args "-v /tmp/maven:/home/jenkins -e MAVEN_CONFIG=/home/jenkins"
        }
    }
    
    stages {
        stage("Build") {
            steps {
                sh "mvn -version"
                sh "echo id = $(id)"
                sh "mvn clean compile"
            }
        }
        
        stage("Test") {
            steps {
                sh "mvn test"
            }
        }

        stage("SonarAnalysis") {
            agent { label "docker" }
            steps {
                sh "echo to be implemented"
                // Uncomment the following lines if SonarQube is configured:
                // def scannerHome = tool 'SonarQubeScanner'
                // withSonarQubeEnv("SonarServer") {
                //     sh "${scannerHome}/bin/sonar-scanner"
                // }
            }
        }

        stage("Deploy") {
            steps {
                sh "mvn install"
            }
        }
    }
    
    post {
        always {
            cleanWs()
        }
    }
}
