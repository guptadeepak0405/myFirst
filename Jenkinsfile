pipeline {
    agent any

    tools {
        maven 'Maven 3.8.8' // Make sure this name matches the Maven version configured in Jenkins
    }

    environment {
        TOMCAT_URL = 'http://localhost:9090/manager/text'
        TOMCAT_CREDENTIALS = 'tomcat-credentials'
    }

    stages {
        stage('Clone Code') {
            steps {
                git 'https://github.com/archis04/myfirst.git'
            }
        }

        stage('Build WAR') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Deploy to Tomcat') {
            steps {
                deploy adapters: [tomcat9(credentialsId: "${TOMCAT_CREDENTIALS}", url: "${TOMCAT_URL}")], contextPath: 'myfirst', war: 'target/myfirst-1.0-SNAPSHOT.war'
            }
        }
    }
}
