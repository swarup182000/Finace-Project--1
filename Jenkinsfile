pipeline {
    agent any

    tools {
        maven 'Maven3'
        jdk 'JDK17'
    }

    stages {
        stage('Checkout the code from GitHub') {
            steps {
                git url: 'https://github.com/swarup182000/Finace-Project--1'
                echo 'FinanceMe project checked out'
            }
        }

        stage('Compile') {
            steps {
                echo 'Compiling code...'
                sh 'mvn compile'
            }
        }

        stage('Test') {
            steps {
                echo 'Running tests...'
                sh 'mvn test'
            }
        }

        stage('CheckStyle') {
            steps {
                echo 'Running QA checks...'
                sh 'mvn checkstyle:checkstyle'
            }
        }

        stage('Package') {
            steps {
                echo 'Packaging...'
                sh 'mvn package'
            }
        }

        stage('Docker Build') {
            steps {
                echo 'Building Docker image...'
                sh 'docker build -t finance-me:latest .'
            }
        }

        stage('Run Docker') {
            steps {
                echo 'Running Docker container...'
                sh 'docker run -dt -p 8091:8091 --name finance-container finance-me:latest'
            }
        }
    }
}
