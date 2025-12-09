#!groovy

pipeline {
  agent any

  stages {
    stage("Build and up") {
      steps {
        sh "npm run build"
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
                  sourceFiles: './dist/*')
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


