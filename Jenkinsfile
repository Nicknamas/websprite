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
        sshPublisher(publishers: [sshPublisherDesc(configName: 'production-server', transfers: [sshTransfer(cleanRemote: false, excludes: '', execCommand: '''docker load -i /var/www/html/*.tar
docker run -d websprite''', execTimeout: 120000, flatten: false, makeEmptyDirs: false, noDefaultExcludes: false, patternSeparator: '[, ]+', remoteDirectory: '', remoteDirectorySDF: false, removePrefix: '', sourceFiles: '*.tar')], usePromotionTimestamp: false, useWorkspaceInPromotion: false, verbose: false)])
      }
    }
  }
}


