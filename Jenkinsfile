pipeline {
    agent {
        docker {
            image 'maven:3.9.0-eclipse-temurin-17'
            args '-v /root/.m2:/root/.m2 --link sonarqube:sonarqube --network environment_default'
        }
    }
    stages {
        stage('Preparation') {
            steps {
                git 'https://github.com/beacon-hash/java-hello-world.git'
            }
        }
        stage('Unit Test') {
            steps {
                sh 'mvn test'
            }
            post {
                always {
                    junit 'server/target/surefire-reports/*.xml'
                }
            }
        }
        stage('Integration Test') {
            steps {
                sh 'mvn verify -DskipUnitTests'
            }
        }
        stage('Build') {
            steps {
                sh 'mvn -Dserver.port=7070 clean install'
            }
        }
        stage('Static Code Analysis') {
            steps {
                withSonarQubeEnv(credentialsId: 'sonarqube-token', installationName: 'Sonarqube Server') {
                    sh 'mvn sonar:sonar clean package'
                }
            }
        }
    }
}