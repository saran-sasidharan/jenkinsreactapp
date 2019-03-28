pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        sh 'npm install'
        echo 'NPM Packages have been loaded...'
      }
    }
    stage('Test') {
      steps {
        sh 'bash ./jenkins/scripts/test.sh'
        input(message: 'Is Test Successful and ready to continue?', ok: 'Yes and Continue to Publish and Execute')
      }
    }
    stage('Deliver and Stop') {
      steps {
        sh 'bash ./jenkins/scripts/deliver.sh'
        input(message: 'Have you tested react application?', ok: 'Yes, I\'ve succesfully tested and continue to stop the server')
        sh 'bash ./jenkins/scripts/kill.sh'
      }
    }
  }
  environment {
    CI = 'true'
    HOME = '.'
    PORT_NUMBER = '9090'
  }
}