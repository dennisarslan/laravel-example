#!/usr/bin/env groovy
def jenkinsFile
stage('Loading Jenkins file') {
  jenkinsFile = fileLoader.fromGit('Jenkinsfile.example', 'git@github.com:dennisarslan/laravel-distro.git', 'develop', null, '')
}

jenkinsFile.start()
