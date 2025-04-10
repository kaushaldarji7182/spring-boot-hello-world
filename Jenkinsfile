pipeline {
    agent any

    environment {
        IMAGE_NAME = "kaushal2118/module_exam"
        TAG = "latest"
        config_docker_credentials_id = "1"
    }

    stages {

        stage('Git Cloning') {
            steps {
                git branch: 'master', url: 'https://github.com/kaushaldarji7182/spring-boot-hello-world.git'
            }
        }

        stage('Login & Push Docker Image') {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: "${config_docker_credentials_id}",
                    usernameVariable: 'DOCKER_USER',
                    passwordVariable: 'DOCKER_PASS'
                )]) {
                    sh """
                        echo $DOCKER_PASS | docker login -u $DOCKER_USER --password-stdin
                        docker build -t ${IMAGE_NAME}:${TAG} .
                        docker push ${IMAGE_NAME}:${TAG}
                    """
                }
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                sh """
                    kubectl delete deployment hello-world-deployment || true
                    kubectl apply -f deployment.yaml
                    kubectl apply -f service.yaml
                """
            }
        }
    }
}
