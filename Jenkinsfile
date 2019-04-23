 pipeline {
  agent any
  options {
    buildDiscarder(logRotator(numToKeepStr: '10'))
  }
  environment {
    DOCKER_CREDS = credentials('amazeeiojenkins-dockerhub-password')
    COMPOSE_PROJECT_NAME = "drupaltest-${BUILD_ID}"
  }
  stages {
    stage('Docker login') {
      steps {
        sh """
        docker login --username amazeeiojenkins --password $DOCKER_CREDS
        """
      }
    }
    stage('Docker Build') {
      steps {
        sh '''
        docker network create amazeeio-network || true
        docker-compose config -q
        docker-compose down
        docker-compose up -d --build "$@"
        '''
      }
    }
    stage('Waiting') {
      steps {
        sh """
        sleep 1s
        """
      }
    }
    stage('Verification') {
      steps {
        sh '''
        docker-compose exec -T blog php -r \"file_exists('.env') || copy('.env.example', '.env');\"
        docker-compose exec -T blog php artisan key:generate --ansi
        echo docker-compose exec -T blog ls -al storage/logs
        echo docker-compose exec -T blog cat storage/logs/laravel-2019-04-23.log
        docker-compose exec -T blog curl http://nginx:8000 -v
        docker-compose down
        '''
      }
    }
  }
}
