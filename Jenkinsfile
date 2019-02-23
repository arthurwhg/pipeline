pipeline {
  agent any
  stages {
    stage('Approve') {
      parallel {
        stage('Approve') {
          steps {
            sh 'echo \'Approval\''
            timestamps()
            timeout(time: 2, activity: true)
          }
        }
        stage('Manager Approve') {
          steps {
            echo 'Manager Approval'
          }
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