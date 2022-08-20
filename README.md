Continuous Integration Pipeline - VCS (Github) > Fetch > Build > Test > Notify (devs)\
Freestyle Jobs - Graphical jobs, good for learning/understanding Jenkins, not recommended\
Pipeline as a Code - Pipeline created in groovy, recommended to do this
- Edit jenkinsfile to define the pipeline, language similar to groovy
- Declarative is the syntax we use
- Pipeline Concepts - Pipeline, Node/Agent, Stage, Step
```
Pipeline {
 Agent { what agent will run this pipeline
 Tools { what tools/plugins are being used
 Environment { environment variables to be called
 Stages {  steps to execute in job (Clone from VCS, Build Maven, Test, etc)
```

Pipeline for Course
```
Developer - Push code to GitHub
Jenkins - Fetch (Git) > Build (Maven) > Unit Test (Maven) > Code Analysis (SonarQube) > Artifact Upload (NexusOSS)
Code Analysis (SonarQube) - Detects vulnerabilities and best practices
Instal SonarQube scanner in the jenkins server and integrate with SonarQube server (manage plugins and such in Jenkins, use token auth via sonarqube)
Quality Gate - Set metrics to pass the code through during analysis (like bugs > 60)
Nexus OSS - Upload artifact here in the last stage of CI pipeline, can also store dependencies for us
```
Create a repository as ‘hosted’ to store artifacts in Nexus, and ‘proxy’ to download dependencies\
Add a notification plugin to Jenkins for automated notification of build status, like to Slack\
Can also use Docker Build to push artifact to ECR for Cloud repository\
Build Triggers automate the build process by using one of the below
- Git Webhook 
- Poll SCM (Jenkins checks in intervals for new commit)
- Scheduled Jobs
- Remote Triggers (Trigger from anywhere) (API Token and CRUMB req)
- Build after other projects are built

Master/Slave Nodes are great for distributed loads, cross platform builds, or software testing
- Master - Chooses what slave node to execute job on
- Slave - Can be anywhere (Windows, Linux, Mac, etc), needs own user and dir on node
