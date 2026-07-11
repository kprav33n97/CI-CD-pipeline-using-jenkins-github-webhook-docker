pipeline {
    agent any

    environment {
        CONTAINER_NAME = "nestjs-app"
        IMAGE_NAME = "nestjs-image"
        EMAIL = "kpraveenkumar2006@gmail.com"
        PORT = "3000"
    }

    stages {
      stage('Clone repo'){
        steps {
            git branch: 'main', url: 'https://github.com/kprav33n97/        CI-CD-pipeline-using-jenkins-github-webhook-docker'
        }
      }

      stage('Build Docker Image') {
        steps {
            sh 'docker build -t $IMAGE_NAME .'
        }
      }

      stage('Stop and remove previous container') {
        steps {
            sh '''
            docker stop $CONTAINER_NAME || true
            docker rm $CONTAINER_NAME || true
            '''
        }
      }

      stage('Docker container run') {
        steps {
            sh '''
            docker run -d -p ${PORT}:${PORT} --name $CONTAINER_NAME $IMAGE_NAME
            '''
        }
      }

      stage('Send email notification') {
        steps {
            emailtext(
                subject:"Nest app deployed successfully"
                body:"The Nest app has been deployed successfully and is running on port ${PORT}."
                to: "${EMAIL}"
            )
        }
      }
} }