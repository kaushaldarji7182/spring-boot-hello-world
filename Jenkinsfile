@Library('shared@main') _
pipeline {
    agent any

    tools {
        // Install the Maven version configured as "M3" and add it to the path.
        maven "m3"
    }
    stages{
        stage("checkout stage"){
            steps{
                checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/kaushaldarji7182/spring-boot-hello-world.git']])
                sh 'mvn clean install'
            }
        }
        stage('docker build step'){
            steps{
                script{
                    sh 'docker build -t kaushal2118/noneimage .'
                }
            }
        }
        stage("docker login and push steps"){
            steps{
                script{
                    withCredentials([string(credentialsId: 'dockerpass', variable: 'dockerpass')]) {
                    sh ' docker login -u kaushal2118 -p $dockerpass'
                    sh ' docker push kaushal2118/noneimage'
                    }
                }
            }
        }
        stage("deployment phase"){
            steps{
                script{
                    sh '''
                     kubectl apply -f deployment.yaml
                    kubectl apply -f service.yaml
                    '''
                }
            }
        }
	stage("groovy"){
	steps{
	script{
			kaushal()
		}
	}	
	}
    }
}

