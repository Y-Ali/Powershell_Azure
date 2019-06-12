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


