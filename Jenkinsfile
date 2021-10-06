pipeline {
  agent {
    docker {
      image 'node:lts-alpine3.14'
      args '-p 3000:3000'
    }

  }
  stages {
    stage('Build') {
      steps {
        sh 'npm install'
      }
    }

    stage('Test') {
      steps {
        sh '''
                    chmod +x \'./jenkins/scripts/test.sh\'
                    \'./jenkins/scripts/test.sh\'
                   '''
      }
    }

    stage('Deliver') {
      steps {
        sh '''
                    chmod +x \'./jenkins/scripts/deliver.sh\'
                   \'./jenkins/scripts/deliver.sh\' 
                '''
        input '¿Terminaste de usar el sitio Web? (Da click en "Proceed" para continuar)'
        sh '''
                   chmod +x \'./jenkins/scripts/kill.sh\'
                   \'./jenkins/scripts/kill.sh\'
                   '''
      }
    }

  }
  environment {
    CI = 'true'
  }
}