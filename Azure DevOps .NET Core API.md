```yaml
trigger:
- master

pool:
  vmImage: 'ubuntu-latest'
  
variables:
  buildConfiguration: 'Release'

steps:
- task: DotNetCoreCLI@2
  inputs:
    command: restore
    projects: '**/*.csproj'
- task: PowerShell@2
  inputs:
    targetType: 'inline'
    script: |
      $paths = Get-ChildItem -include *.csproj -Recurse
             foreach($pathobject in $paths) 
             {
                 $path = $pathobject.fullname
                 $doc = New-Object System.Xml.XmlDocument
                 $doc.Load($path)
                 $child = $doc.CreateElement("ProjectGuid")
                 $child.InnerText = [guid]::NewGuid().ToString().ToUpper()
                 $node = $doc.SelectSingleNode("//Project/PropertyGroup")
                 $node.AppendChild($child)
                 $doc.Save($path)
             }
- task: SonarCloudPrepare@1
  inputs:
    SonarCloud: 'SonarCloudConnection'
    organization: 'kemmita'
    scannerMode: 'MSBuild'
    projectKey: 'apidevopstest'
- task: DotNetCoreCLI@2
  displayName: Build
  inputs:
    command: build
    projects: '**/api/*.csproj'
    arguments: '--configuration $(buildConfiguration)'

- task: DotNetCoreCLI@2
  inputs:
    command: test
    projects: '**/*Tests/*.csproj'
    arguments: '--configuration $(buildConfiguration)'

- task: DotNetCoreCLI@2
  displayName: 'dotnet publish'
  inputs: 
    command: publish
    publishWebProjects: false
    projects: '**/api/*.csproj'
    arguments: '--configuration $(buildConfiguration) --output $(Build.ArtifactStagingDirectory)'
    zipAfterPublish: true
- task: SonarCloudAnalyze@1
- task: SonarCloudPublish@1
  inputs:
    pollingTimeoutSec: '300'
- task: PublishBuildArtifacts@1
  displayName: 'publish artifacts'
```
