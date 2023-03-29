pipeline {
    agent any
    stages {
        stage('Clone stage') {
            steps {
                git 'https://github.com/dosehieu/simple-nodejs-app.git'
            }
        }
        stage('Build stage') {
            steps {
                withDockerRegistry(credentialsId: 'docker-hub', url: 'https://index.docker.io/v1/') {
                    sh label: '', script: 'docker build -t dosehieu/test-node:v1 .'
                    sh label: '', script: 'docker push dosehieu/test-node:v1'
                }
            }
        }
        stage('SSH server stage') {
            steps {
                sshagent(['ssh-remote']) {
                    sh 'ssh -o StrictHostKeyChecking=no -l root 172.16.10.102 touch test.txt'
                }
            }
        }
    }
}