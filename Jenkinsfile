pipeline {
    agent {
        label 'ansible'
    }
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
        stage ('Pre-deploy') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub', passwordVariable: 'password', usernameVariable: 'username')]) {
                    sh 'ANSIBLE_CONFIG=ansible/ansible.cfg ansible-playbook --extra-vars "dockerhub_username=$username dockerhub_password=$password workspace=$WORKSPACE build_number=$BUILD_ID" ansible/site.yml'
                }
            }
        }
    }
}