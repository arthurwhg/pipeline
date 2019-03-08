pipeline {
  agent any
  stages {
    stage('Approve') {
      parallel {
        stage('Approve') {
          steps {
            sh 'echo \'Approval\''
            timestamps() {
              echo 'Within Timestamp'
            }

            timeout(time: 2, activity: true) {
              sleep 5
            }

          }
        }
        stage('JIRA') {
          steps {
            script {
              def testIssue = [fields: [ // id or key must present for project.
              project: [key: 'WBXCLDMGMT'],
              summary: 'New JIRA Created from Jenkins.',
              description: 'New JIRA Created from Jenkins.',
              //customfield_1000: 'customValue',
              // id or name must present for issueType.
              issuetype: [name: 'Task']]]

              response = jiraNewIssue issue: testIssue, site: 'DEV'
	      //response = jiraGetIssue idOrKey: 'TESTSPARK-11', site: 'DEV' 
	
              echo response.successful.toString()
              echo response.data.toString()
            }

          }
        }
        stage('Manager Approve') {
          steps {
	    script {
              echo 'Get issue'
              def response = jiraGetFields idOrKey: 'WBXCLDMGMT-908', site: 'DEV'
	      echo "result"
              echo response.successful.toString()
              echo "Data" 
              echo response.data.toString()
              echo response.data.Status.toString()
            }
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
