---
title: Example of Xamarin iOS with Cake
date: '2016-07-11 00:00:00'
categories: xamarin ios cake devops
layout: post
---
```csharp
#addin "Cake.FileHelpers"
#addin "Cake.Plist"

var assemblyInfoFile = File("./src/CommonAssemblyInfo.cs");
var plistFile = File("./src/MyCoolApplication.iOS/Info.plist");
var projectFile = File("./src/MyCoolApplication.iOS/MyCoolApplication.iOS.csproj");
var solutionFile = File("./src/MyCoolApplication.sln");

// should MSBuild treat any errors as warnings.
var treatWarningsAsErrors = "false";

// Parse release notes
var releaseNotes = ParseReleaseNotes("./RELEASENOTES.md");

// Get version
var version = releaseNotes.Version.ToString();
var epoch = (long)(DateTime.UtcNow - new DateTime(1970, 1, 1)).TotalSeconds;
var semVersion = local ? string.Format("{0}.{1}", version, epoch) : string.Format("{0}.{1}", version, epoch);

Task("Build")
    .IsDependentOn("RestoreAssets")
    .IsDependentOn("RestoreComponents")
    .IsDependentOn("RestorePackages")
    .IsDependentOn("UpdateAssemblyInfo")
    .IsDependentOn("UpdateApplePlist")
    .Does (() =>
{

    DotNetBuild(projectFile, settings =>
      settings.SetConfiguration("Debug")
          .WithProperty("Platform", "iPhoneSimulator")
          .WithProperty("OutputPath", "bin/Simulator/")
          .WithProperty("TreatWarningsAsErrors", treatWarningsAsErrors));

    DotNetBuild(projectFile, settings =>
      settings.SetConfiguration("AppStore")
          .WithProperty("Platform", "iPhone")
          .WithProperty("OutputPath", "bin/AppStore/")
          .WithProperty("TreatWarningsAsErrors", treatWarningsAsErrors));
});

Task("UpdateApplePlist")
    .Does (() =>
{
    dynamic plist = DeserializePlist(plistFile);

    plist["CFBundleShortVersionString"] = version;
    plist["CFBundleVersion"] = semVersion;

    SerializePlist(plistFile, plist);
});

Task("UpdateAssemblyInfo")
    .Does (() =>
{
    CreateAssemblyInfo(assemblyInfoFile, new AssemblyInfoSettings() {
        Product = "Geoffrey Huntley",
        Version = version,
        FileVersion = version,
        InformationalVersion = semVersion,
        Copyright = "Copyright (c) Geoffrey Huntley"
    });
});

Task("RestoreComponents")
    .Does(() =>
{
    var username = EnvironmentVariable("XAMARIN_USERNAME");
    if (string.IsNullOrEmpty(username))
    {
        throw new Exception("The XAMARIN_USERNAME environment variable is not defined.");
    }

    var password = EnvironmentVariable("XAMARIN_PASSWORD");
    if (string.IsNullOrEmpty(password))
    {
        throw new Exception("The XAMARIN_PASSWORD environment variable is not defined.");
    }

    RestoreComponents(solutionFile, new XamarinComponentRestoreSettings()
    {
        ToolPath = "./tools/xamarin-component/xamarin-component.exe",
        Email = username,
        Password = password
    });
});

Task("RestorePackages")
    .Does (() =>
{
    NuGetRestore(solutionFile);
});

RunTarget(build);
```
