# pipeline

A Jenkins pipeline leverages Jira Steps plugin to create issue in Jira and retrieve the status. 

It is a sample pipeline. When timeout, the pipeline continue the next step and fail the step checking status from Jira. 

The possible way is to use webhook to trigger a pipeline after status changed. 

