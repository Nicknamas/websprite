#!groovy

pipeline {
  agent any

  stages {
    stage("Build and save") {
      steps {
        sh "docker build -t websprite:latest ."
        sh "docker save -o websprite.tar websprite:latest"
        sh "ls -la"
      }
    }
    stage("Deploy") {
      steps {
        sshPublisher(
          publishers: [
            sshPublisherDesc(
              configName: 'production-server', 
              transfers: [
                sshTransfer(
                  execCommand: 'docker load -i websprite.tar websprite:latest',
                  remoteDirectory: '', 
                  removePrefix: '', 
                  sourceFiles: '*.tar'
                )
              ], 
            )
          ]
        )
      }
    }
  }
}


