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
	
              //echo response.successful.toString()
              //echo response.data.toString()

	      currentBuild.description = response.data.key
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
              echo "Fields" 
              //echo response.data.toString()
              def fields = ''
	      for (item in response.data) {
		 fields = fields +  item.id + '--' + item.name + '\n'
		}
	      echo fields
            }
          }
        }
      }
    }
    stage('QA') {
      steps {
        echo 'Now QA'
            script {
              def issueKey = currentBuild.description
              echo 'Get Transitions ' + issueKey + '!'
              response = jiraGetIssueTransitions idOrKey: issueKey, site: 'DEV'
	      //echo response.data.transitions.toString()
	      def transitions = '@'
	      for (item in response.data.transitions) {	
		transitions = transitions + "->" + item.name
		}
	      echo transitions
            }
      }
    }
    stage('ATS') {
      steps {
        echo "ATS"
            script {
              def issueKey = currentBuild.description
              echo 'Get Issue'
              response = jiraGetIssue idOrKey: issueKey, site: 'DEV'
              //echo response.toString()
		echo "Initiated status is " + response.data.fields.status.name
		echo response.data.fields.priority.name
            }
      }
    }
    stage('BTS') {
      steps {
        echo "BTS"
            script {
              def issueKey = currentBuild.description
              echo 'Wait for apporval'
              response = jiraGetIssue idOrKey: issueKey, site: 'DEV'
                echo "Initiated status is " + response.data.fields.status.name
                echo "Initiated priority is " + response.data.fields.priority.name

		//check approval
              for ( ; response.data.fields.status.name != 'Done'; ) {
		// check every 30 seconds
		timeout(time: 2, activity: true) {
              		sleep 30 
            	 }
                response = jiraGetIssue idOrKey: issueKey, site: 'DEV'
                //echo 'now status ' + response.data.fields.status.name
              }
            }

      }
    }
    stage('PROD') {
      steps {
        echo "PROD"
      }
    }
  }
}
