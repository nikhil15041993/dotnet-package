

## Prerequisites
* Install .NET SDK: Ensure you have the .NET SDK installed. You can download it from the .NET Download page.

* Install Git: Ensure you have Git installed. You can download it from the Git website.

* GitHub Account: Ensure you have a GitHub account and have created a repository to publish your package.

## Step 1: Create a New .NET Project
First, open a terminal or command prompt and create a new .NET class library project.

```
dotnet new classlib -n MyAwesomeLibrary
cd MyAwesomeLibrary
```
This command creates a new class library named MyAwesomeLibrary and navigates into the project directory.

## Step 2: Write Your Library Code
Open the generated Class1.cs file in the MyAwesomeLibrary directory and write your library code. For example:

```
namespace MyAwesomeLibrary
{
    public class Class1
    {
        public string SayHello()
        {
            return "Hello, World!";
        }
    }
}
```

## Step 3: Create the NuGet Package
Before creating the package, you need to edit the .csproj file to include metadata required for NuGet.

Open ```MyAwesomeLibrary.csproj``` and add the following properties inside the <Project> tag:

```
<PropertyGroup>
  <PackageId>MyAwesomeLibrary</PackageId>
  <Version>1.0.0</Version>
  <Authors>YourName</Authors>
  <Company>YourCompany</Company>
  <Description>This is a sample description for MyAwesomeLibrary.</Description>
  <PackageTags>sample;library;dotnet</PackageTags>
  <PackageLicenseExpression>MIT</PackageLicenseExpression>
  <RepositoryUrl>https://github.com/YourUsername/YourRepository</RepositoryUrl>
</PropertyGroup>
```

## Build the NuGet package:

```
dotnet pack --configuration Release
```
This command generates a NuGet package (.nupkg file) in the bin/Release directory.

## Step 4: Publish to GitHub Packages
Authenticate with GitHub: Create a personal access token on GitHub with the write:packages scope.

Configure NuGet to use GitHub Packages: Add the GitHub Packages source to your NuGet configuration.

Create or edit a ```NuGet.config``` file in your project directory and add the following:

```
<?xml version="1.0" encoding="utf-8"?>
<configuration>
  <packageSources>
    <add key="github" value="https://nuget.pkg.github.com/githubYourUsername/index.json" />
  </packageSources>
  <packageSourceCredentials>
    <github>
      <add key="Username" value="YourUsername" />
      <add key="ClearTextPassword" value="YourGitHubPAT" />
    </github>
  </packageSourceCredentials>
</configuration>
```
Replace <project_id> with your GitLab project's ID, which you can find in your project’s “Settings” > “General” page.

### Publish to GitLab Package Registry

1. Create a GitLab Personal Access Token (PAT)
Go to your GitLab Profile.
Generate a token with the ```write_package_registry``` scope.

```
<?xml version="1.0" encoding="utf-8"?>
<configuration>
  <packageSources>
    <add key="gitlab" value="https://gitlab.com/api/v4/projects/<project_id>/packages/nuget/index.json" />
  </packageSources>
  <packageSourceCredentials>
    <gitlab>
      <add key="Username" value="YourGitLabUsername" />
      <add key="ClearTextPassword" value="YourGitLabPAT" />
    </gitlab>
  </packageSourceCredentials>
</configuration>

```

Replace YourUsername with your GitHub username and YourGitHubPAT with your personal access token.

Publish the Package: Use the dotnet nuget push command to publish the package.

```
dotnet nuget push bin/Release/MyAwesomeLibrary.1.0.0.nupkg --source github
```

## Step 5: Verify the Package on GitHub
Go to your GitHub repository and navigate to the "Packages" section to verify that your NuGet package has been published.

Example Project Structure
Your project structure should look like this:

```
MyAwesomeLibrary/
├── MyAwesomeLibrary.csproj
├── Class1.cs
├── NuGet.config
└── bin/
    └── Release/
        └── MyAwesomeLibrary.1.0.0.nupkg
```
