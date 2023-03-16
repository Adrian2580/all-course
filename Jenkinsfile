#!/usr/bin/env groovy

pipeline {
    agent any
    stages {
        stage('build') {
            steps {
                script {
                    echo "Building the application..."
                }
            }
        }
        stage('test') {
            steps {
                script {
                    echo "Testing the application..."
                }
            }
        }
        stage('deploy') {
            steps {
                script {
                    echo "Deploying the application to EC2..."
                    def dockerComposeCommand = "docker-compose -f docker-compose.yaml up --detach"
                    sshagent(['ec2-server-key']){
                        sh "scp docker-compose.yaml ec2-user@52.57.154.251:/home/ec2-user"
                        sh "ssh -o StrictHostKeyChecking=no ec2-user@52.57.154.251 ${dockerComposeCommand}"
                    }
                }
            }
        }
    }
}
