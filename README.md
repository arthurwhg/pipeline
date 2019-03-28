# pipeline

A Jenkins pipeline leverages Jira Steps plugin to create issue in Jira and retrieve the status. 

It is a sample pipeline. When timeout, the pipeline continue the next step and fail the step checking status from Jira. 

The possible way is to use webhook to trigger a pipeline after status changed. 

Sample code:


              def testIssue = [fields: [      // id or key must present for project.
                project: [key: 'WBXCLDMGMT'],
                summary: 'New JIRA Created from Jenkins.',
                description: 'New JIRA Created from Jenkins. Project name is ' + currentBuild.projectName + '. build ID is ' + currentBuild.id,
                issuetype: [name: 'Task']]]   // Issue type is Task

              // Site is the Jira Step configuration site name
              response = jiraNewIssue issue: testIssue, site: 'DEV'
	
              // Use global paramenter to pass the issue key to be used in the next steps
	            currentBuild.description = response.data.key
