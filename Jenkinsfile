pipeline {

  agent any

  stages {

    stage('git cloninig') {

      steps {

        git branch: 'Feature', url:'https://github.com/kaushaldarji7182/spring-boot-hello-world.git'

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
