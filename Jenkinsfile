pipeline {
    agent any
    tools {
        maven 'maven-3.8.7'
    }
    stages {
        stage ('Preparation') {
            steps {
                git "https://github.com/beacon-hash/java-hello-world.git"
            }
        }
        stage ('Build') {
            steps {
                sh 'mvn clean install'
            }
        }
        stage ('Deploy') {
            steps {
                deploy adapters: [tomcat8(credentialsId: 'tomcat-credentials', path: '', url: 'http://tomcat:8080/')], war: '**/*.war'
            }
        }
    }
}