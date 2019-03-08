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
	  step {
	    def testIssue = [fields: [ // id or key must present for project.
        	                       project: [key: 'WBXCLDMGMT'],
                	               summary: 'New JIRA Created from Jenkins.',
                        	       description: 'New JIRA Created from Jenkins.',
                 	               //customfield_1000: 'customValue',
                         	      // id or name must present for issueType.
                            	       issuetype: [name: 'task']]]

	    response = jiraNewIssue issue: testIssue

	    echo response.successful.toString()
	    echo response.data.toString()
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
