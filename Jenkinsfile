pipeline {
    agent {
        docker {
            image 'maven:3.9.0-eclipse-temurin-17'
            args '-v /root/.m2:/root/.m2'
        }
    }
    stages {
        stage('Preparation') {
            steps {
                git 'https://github.com/beacon-hash/java-hello-world.git'
            }
        }
        stage('Test') {
            steps {
                sh 'mvn test'
                sh 'ls -lR *'
            }
            // post {
            //     always {
            //         junit 'target'
            //     }
            // }
        }
    }
}