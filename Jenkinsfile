pipeline {
    agent any

    tools {
        maven 'maven3'
    }

    stages {
        stage('Build') {
            steps {
                checkout scmGit(
                    branches: [[name: '*/main']],
                    extensions: [],
                    userRemoteConfigs: [[url: 'https://github.com/kaushaldarji7182/spring-boot-hello-world.git']]
                )
                sh 'mvn clean install'
            }
        }

        stage('Docker Image') {
            steps {
                script {
                    sh 'docker build -t kaushal2118/my_image2118 .'
                }
            }
        }

        stage('Push Docker Image') {
            steps {
                script {
                    withCredentials([string(credentialsId: 'dockerhubpwd', variable: 'dockerhubpwd')]) {
                        sh 'docker login -u kaushal2118 -p $dockerhubpwd'
                        sh 'docker push kaushal2118/my_image2118'
                    }
                }
            }
        }
    }
}

