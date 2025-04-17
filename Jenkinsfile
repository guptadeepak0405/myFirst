pipeline {
    agent any

    tools {
        maven 'Maven' // Make sure this name matches the Maven version configured in Jenkins
    }

    environment {
        TOMCAT_URL = 'http://localhost:9090/manager/text'
        TOMCAT_CREDENTIALS = 'tomcat-credentials'
    }

    stages {
        stage('Clone Code') {
            steps {
                git branch: 'main', url: 'https://github.com/guptadeepak0405/myFirst.git'
            }
        }

        stage('Build WAR') {
            steps {
                bat 'mvn clean package'
            }
        }

        stage('Deploy to Tomcat') {
            steps {
                deploy adapters: [
                    tomcat9(
                        credentialsId: "${TOMCAT_CREDENTIALS}",
                        url: "${TOMCAT_URL}"
                    )
                ], contextPath: 'myfirst', war: 'target/myfirst.war'
            }
        }
    }
}
