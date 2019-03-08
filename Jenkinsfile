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

              //response = jiraNewIssue issue: testIssue, site: 'DEV'
	      //response = jiraGetIssue idOrKey: 'TESTSPARK-11', site: 'DEV' 
	
              //echo response.successful.toString()
              //echo response.data.toString()
	      //echo response.data.key
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
              //echo response.data.toString()
	      //echo response.toString()
            }
          }
        }
      }
    }
    stage('QA') {
      steps {
        echo 'Now QA'
            script {
              echo 'Get Transitions'
              response = jiraGetIssueTransitions idOrKey: 'WBXCLDMGMT-908', site: 'DEV'
	      //echo response.data.transitions.toString()
	      for (item in response.data.transitions) {	
			echo item.name
		}
            }
      }
    }
    stage('ATS') {
      steps {
        echo "ATS"
            script {
              echo 'Get Issue'
              response = jiraGetIssue idOrKey: 'WBXCLDMGMT-908', site: 'DEV'
              //echo response.data.toString()
              for (item in response.data) { 
                        echo item.id 
                }
            }
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
