pipeline {
  agent any
  stages {
    stage('Approve') {
      steps {
        sh 'echo \'Approval\''
        timestamps() {
          echo 'Within loop'
        }

      }
    }
    stage('QA') {
      steps {
        echo 'Now QA'
      }
    }
    stage('ATS') {
      steps {
        sh 'echo "ATS"'
      }
    }
    stage('BTS') {
      steps {
        sh 'echo "BTS"'
      }
    }
    stage('PROD') {
      steps {
        sh 'echo "PROD"'
      }
    }
  }
}