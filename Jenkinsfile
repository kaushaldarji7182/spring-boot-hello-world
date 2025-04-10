pipeline {

  agent any

  stages {

    stage('git cloning') {

      steps {
        git branch: 'feature', url:'https://github.com/kaushaldarji7182/spring-boot-hello-world.git'
      }

    }

    stage('Building jar file for project') {

      steps {
        sh "mvn dependency:go-offline"
        sh "mvn clean package -DskipTests"
      }

    }
  }
}
