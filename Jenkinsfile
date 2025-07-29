pipeline {
  agent { label 'dev' }

  environment {
    IMAGE_NAME = "fastapi-jenkins"
    CONTAINER_NAME = "fastapi_app"
    APP_PORT = "8000"
  }

  stages {
    stage('Checkout') {
      steps {
        git url: 'https://github.com/rameshdurgam115/JenkinsCICDREPO.git', credentialsId: 'github-pat'
      }
    }

    stage('Deploy with Docker Compose') {
      steps {
        echo "🔄 Stopping any existing containers"
        sh 'docker compose down || true'

        echo "🐳 Building Docker images"
        sh 'docker compose build'

        echo "🚀 Starting containers"
        sh 'docker compose up -d'
      }
    }
  }

  post {
    success {
      echo "✅ Deployment succeeded. Access app via http://192.168.128.172:80"
    }
    failure {
      echo "❌ Deployment failed. Check Jenkins logs."
    }
  }
}
