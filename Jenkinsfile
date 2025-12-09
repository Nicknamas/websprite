#!groovy

def agentLabel = "prod"

pipeline {
  agent { label agentLabel }

  stages {
    stage("Build and up") {
      steps {
        sh "docker compose up --build"
      }
    }
  }
}
