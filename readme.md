## CI-CD-CD with Azure Devops for ASP.NetCore Web Application

Steps:

1. Create a new project.

2. Visibility: Make it private (or public if you want everyone to see it) 

3. Select Git as the Version Control

4. In Azure DevOps, Select ‘repositories’

5. In Powershell: `cd` into your project folder. Then in the ‘repositories’ tab (in Azure DevOps) copy the HTTPS commands into powershell. 

      For example:

      `git remote add origin https://yousufali@dev.azure.com/yousufali/Student%20Portal%20Project/_git/Student%Portal%20Project`

      `git add .`

      `git commit -m “first commit”`

      `git push origin master`

6. Refresh your Azure Devops page. In your repositories, you should now see your project files.

7. Select Pipelines > Builds 

8. Select Azure Reps and select your repository.

9. Choose Template: ASP.Net Core, or the template you need for your project.

10. You should see a azure-pipelines.yml file. For now keep this as default as this is enough for a build. 

11. Save and run.

12. To have a web app in Azure, we need 3 things: a resource group, a resource plan, and a web app.

13. First create a resource group. In powershshell type:

	`az group create —name projectresourcegroup —location eastus`
      
14. This will create a resource group called projectresourcegroup, in the location eastus.

15. To create a plan, In powershell type:

	`az appservice plan create —name resourceplan —resource-group projectresourcegroup —sku FREE`
	
16. Finally we need a  webapp:

	`az webapp create —name projectwebapp —resource-group projectresourcegroup —plan resourceplan`

17. If you go to Microsoft Azure, you should see those 3 things created.

18. Great! Now let's go change that YAML file that was created ealier. We need to add tasks that will 'package' our files, create a zip, and then move those files to our artefact folder.

`- task: DotNetCoreCLI@2
  displayName: 'Dotnet Publish'
  inputs:
    command: publish
    publishWebProjects: True
    arguments: '--configuration $(buildConfiguration) --output $(Build.ArtifactStagingDirectory)'
    zipAfterPublish: True`

`- task: PublishBuildArtifacts@1
  displayName: 'Publish Build Artifacts'`

