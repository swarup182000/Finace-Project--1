pipeline {
  agent any

  tools {
    maven 'Maven3'
    jdk 'JDK17'
  }

  stages {
    stage('Checkout') {
      steps {
        git url: 'https://github.com/swarup182000/Finace-Project--1'
      }
    }

    stage('Compile') {
      steps {
        sh 'mvn compile'
      }
    }

    stage('Test') {
      steps {
        sh 'mvn test'
      }
    }

    stage('CheckStyle') {
      steps {
        sh 'mvn checkstyle:checkstyle'
      }
    }

    stage('Package') {
      steps {
        sh 'mvn package'
      }
    }

    stage('Docker Build') {
      steps {
        sh 'docker build -t finance-me:latest .'
      }
    }

    stage('Docker Push') {
      steps {
        withCredentials([usernamePassword(
          credentialsId: '0c7554a4-5a04-4a65-9faf-e61cd8db40ba',
          usernameVariable: 'USERNAME',
          passwordVariable: 'PASSWORD'
        )]) {
          sh '''
            echo "$PASSWORD" | docker login -u "$USERNAME" --password-stdin
            docker tag finance-me:latest $USERNAME/finance-me:latest
            docker push $USERNAME/finance-me:latest
          '''
        }
      }
    }
  }
}
