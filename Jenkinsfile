#!groovy

pipeline {
  agent any

  stages {
    stage("Build and save") {
      steps {
        sh "docker build -t websprite:latest ."
        sh "docker save -o websprite.tar websprite:latest"
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
                  execCommand: 'docker load -i ./websprite.tar && docker run -d websprite:latest', 
                  remoteDirectory: '', 
                  removePrefix: '', 
                  sourceFiles: './websprite.tar'
                )
              ], 
            )
          ]
        )
      }
    }
  }
}


