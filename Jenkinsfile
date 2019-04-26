#!/usr/bin/env groovy
def jenkinsFile
stage('Loading Jenkins file') {
  jenkinsFile = fileLoader.fromGit('testjenkinsstuff/cicd/testMyPipeline', 'git@github.com:dennisarslan/laravel-distro.git', 'develop', null, '')
}

jenkinsFile.start()
