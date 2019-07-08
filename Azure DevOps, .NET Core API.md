1. Go in and create a new repo in Azure devops
2. Create a new pipeline based off of the repo you created and configure it using the .net core yaml file.
3. After you have done the inital build, go back to your code on your machine and pull down the code from the repo "git pull"
4. Next alter your .yml file that was created to look like below
```yml
trigger:
- master

pool:
  vmImage: 'ubuntu-latest'
  
variables:
  buildConfiguration: 'Release'

steps:
- script: dotnet build --configuration $(buildConfiguration)
  displayName: 'dotnet build $(buildConfiguration)'

- task: DotNetCoreCLI@2
  displayName: 'dotnet publish --configuration $(buildConfiguration) --output $(Build.ArtifactStagingDirectory)'
  inputs: 
    command: publish
    publishWebProjects: false
    projects: '**/*.csproj'
    arguments: '--configuration $(buildConfiguration) --output $(Build.ArtifactStagingDirectory)'
    zipAfterPublish: true

- task: PublishBuildArtifacts@1
  displayName: 'publish artifacts'
```
5. Now we need to create a release pipeline, select the "Azure App Service deployment"
6. In stages, click on 1 job, 1 taks.
7. Here you will select your azure plan along with the app type and the actual app.
8. Finaly you will create a Artificat that will trigger the stage, the artifact should be configured to the build we created.
