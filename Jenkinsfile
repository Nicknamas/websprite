#!groovy

pipeline {
  agent any

  stages {
    stage("Build and up") {
      steps {
        sh "ifconfig"
        sh "docker compose up --build -d"
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
                  cleanRemote: false, 
                  excludes: '', 
                  execCommand: '', 
                  execTimeout: 120000, 
                  flatten: false, 
                  makeEmptyDirs: false, 
                  noDefaultExcludes: false, 
                  patternSeparator: '[, ]+', 
                  remoteDirectory: '', 
                  remoteDirectorySDF: false, 
                  removePrefix: '', 
                  sourceFiles: '*')
              ], 
              usePromotionTimestamp: false, 
              useWorkspaceInPromotion: false, verbose: false
            )
          ]
        )
      }
    }
  }
}


