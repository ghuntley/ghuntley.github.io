---
title: Example of Xamarin Android with Cake
date: '2016-07-11 00:00:00'
categories: xamarin android cake devops
layout: post
---
```csharp
#addin "Cake.FileHelpers"
#addin "Cake.AndroidAppManifest"

var manifestFile = File("./src/MyCoolApplication.Droid/Properties/AndroidManifest.xml");
var projectFile = File("./src/MyCoolApplication.Droid/MyCoolApplication.Droid.csproj");
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
    .IsDependentOn("UpdateAndroidManifest")
    .Does (() =>
{
    var keyStore = EnvironmentVariable("ANDROID_KEYSTORE");
    if (string.IsNullOrEmpty(keyStore))
    {
        throw new Exception("The ANDROID_KEYSTORE environment variable is not defined.");
    }

    var keyStoreAlias = EnvironmentVariable("ANDROID_KEYSTORE_ALIAS");
    if (string.IsNullOrEmpty(keyStoreAlias))
    {
        throw new Exception("The ANDROID_KEYSTORE_ALIAS environment variable is not defined.");
    }
    
    var keyStorePassword = EnvironmentVariable("ANDROID_KEYSTORE_PASSWORD");
    if (string.IsNullOrEmpty(keyStorePassword))
    {
        throw new Exception("The ANDROID_KEYSTORE_PASSWORD environment variable is not defined.");
    }


    DotNetBuild(projectFile, settings =>
        settings.SetConfiguration("Debug")
            .WithTarget("SignAndroidPackage")
            .WithProperty("DebugSymbols", "true")
            .WithProperty("DebugType", "Full")
            .WithProperty("OutputPath", "bin/Debug/")
            .WithProperty("TreatWarningsAsErrors", treatWarningsAsErrors));

    // For more information about MSBuild properties and how they function, read:
    // https://developer.xamarin.com/guides/android/under_the_hood/build_process/

    DotNetBuild(projectFile, settings =>
        settings.SetConfiguration("Release")
            .WithTarget("SignAndroidPackage")
            .WithProperty("AndroidKeyStore", "true")
            .WithProperty("AndroidSigningStorePass", keyStorePassword)
            .WithProperty("AndroidSigningKeyStore", keyStore)
            .WithProperty("AndroidSigningKeyAlias", keyStoreAlias)
            .WithProperty("AndroidSigningKeyPass", keyStorePassword)
            .WithProperty("DebugSymbols", "false")
            .WithProperty("OutputPath", "bin/Release/")
            .WithProperty("TreatWarningsAsErrors", treatWarningsAsErrors));
});


Task("UpdateAndroidManifest")
    .Does (() =>
{
    var manifest = DeserializeAppManifest(manifestFile);
    manifest.VersionName = version.ToString();
    manifest.VersionCode = Int32.Parse(manifest.VersionName.Replace(".", string.Empty));

    SerializeAppManifest(manifestFile, manifest);
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

