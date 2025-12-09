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
                  execCommand: 'touch test.text',
                  remoteDirectory: '', 
                  removePrefix: '', 
                  sourceFiles: '*.tar'
                )
              ], 
            )
          ]
        )
        sshagent(credentials : ['production-server']) {
          sh 'ssh -tt jenkins@109.73.196.251 -o StrictHostKeyChecking=no "docker load -i /var/www/html/websprite.tar"'
        }
      }
    }
  }
}


