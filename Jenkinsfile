pipeline {
  agent any
  stages {
    stage('Build and Test') {
      steps {
        script {
          sh './mvn clean package'
        }

      }
    }

    stage('Build Docker Image') {
      steps {
        script {
          dockerImage = docker.build("spring-boot-app")
        }

      }
    }

    stage('Push to Docker Registry') {
      steps {
        script {
          docker.withRegistry('', 'prasanthmeduri') {
            dockerImage.push("${env.BUILD_NUMBER}")
            dockerImage.push("latest")
          }
        }

      }
    }

  }
  post {
    always {
      cleanWs()
    }

  }
}