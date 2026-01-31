pipeline {
  agent any

  environment {
    APP_NAME = "node-app"
    IMAGE_NAME = "demo-node-app:v1"
    APP_PORT = "3000"
  }

  stages {

    stage("Checkout Code") {
      steps {
        echo "Cloning GitHub repository..."
        git branch: "master", url: "https://github.com/VardhanLearn/Dockerized-Jenkins-CI-CD-on-AWS-EC2.git"
      }
    }

    stage("Build Docker Image") {
      steps {
        echo 'Building Docker Image...'
        sh 'docker build -t demo-node-app:v1 .'
      }
    }

    stage("Deploy Container") {
      steps {
        echo "Deploying Docker Container..."
        sh """
          docker stop ${APP_NAME} || true
          docker rm ${APP_NAME} || true
          docker run -d --name ${APP_NAME} -p ${APP_PORT}:${APP_PORT} ${IMAGE_NAME}
        """
      }
    }

    stage("Verify Deployment") {
      steps {
        echo "Checking running containers..."
        sh "docker ps"
      }
    }
  }

  post {
    success {
      echo "✅ Deployment Successful!"
    }
    failure {
      echo "❌ Deployment Failed!"
    }
  }
}
