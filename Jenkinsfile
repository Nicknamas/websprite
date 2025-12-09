#!groovy

pipeline {
  agent any

  stages {
    stage("Build and up") {
      steps {
        sh "docker compose up --build"
        sh "ifconfig"
      }
    }
  }
}

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

