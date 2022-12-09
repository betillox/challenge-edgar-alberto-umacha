pipeline {
    agent {
        label 'prod-nodo'
    }

    stages {

        stage('Compilacion') {
            steps {
               sh 'mvn -D skipTests clean install package'
            }
        }

        stage('Unit test') {
            steps {
                sh 'mvn test'
            }
            post {
                always {
                   junit 'target/surefire-reports/*.xml'
                }
            }
        }

        stage('Build docker image') {
            steps {
                sh 'docker image build -t final-challenge-webapp .'
            }
        }

        stage('Tag docker image') {
            steps {
                sh 'docker image tag final-challenge-webapp betillo/final-challenge-webapp:latest'
            }
        }

        stage('Upload docker image') {
            steps {
          	sh 'docker login -u betillo -p Guitarra123.'
      	  	sh 'docker image push betillo/final-challenge-webapp:latest'
            }
        }
    }
} 


 
