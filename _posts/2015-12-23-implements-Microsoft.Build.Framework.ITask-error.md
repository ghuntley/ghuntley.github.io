---
layout:     post
title:      Implements Microsoft.Build.Framework.ITask Error
date:       2015-12-23
summary:    Now in this particular instance the root course was NuGet wasn't configured correctly and multiple projects had been manually edited to add in the `Microsoft.Bcl.Build` task at a non-standard hard coded location which did not exist because `.gitignore` had been properly configured.  
categories: msbuild nuget visual-studio gitignore dotnet4 rca
---

Inherited a project today which uses the [Async Targeting Pack](https://www.nuget.org/packages/Microsoft.Bcl.Async) to back port `async` and `await` to the .NET 4.0 platform. Anyway, in this instance the `packages.config` was not checked into the version source control and unfortunately the [.gitignore](https://github.com/github/gitignore/blob/master/VisualStudio.gitignore) was appropriately configured to exclude all binaries (as it should be). 

The result? The solution would not compile and needed repairing via installing the appropriate NuGet packages. As .NET 4.0 is being targeted, `Microsoft.Bcl.Build` is needed as an dependency because it contains the MSBuild task that is responsbile for weaving in `Microsoft.Bcl.Async` / providing `async` and `await`.

Now in this particular instance the root course was that NuGet wasn't configured correctly and multiple projects had been manually edited to add in the `Microsoft.Bcl.Build` task at a non-standard hard coded location which did not exist because `.gitignore` had been properly configured.

Frustrating to diagnose:

    The system cannot find the file specified. Confirm that the <UsingTask>
    declaration is correct, that the assembly and all its dependencies are
    available, and that the task contains a public class that implements
    Microsoft.Build.Framework.ITask

Rather easy to fix by editing the `.csproj` and removing the offending manual change:

    <Import Project="..\Libraries\Microsoft.Bcl.Build.1.0.7\tools\Microsoft.Bcl.Build.targets" />
    <Import Project="..\packages\Microsoft.Bcl.Build.1.0.21\build\Microsoft.Bcl.Build.targets" Condition="Exists('..\packages\Microsoft.Bcl.Build.1.0.21\build\Microsoft.Bcl.Build.targets')" />

Becomes

    <Import Project="..\packages\Microsoft.Bcl.Build.1.0.21\build\Microsoft.Bcl.Build.targets" Condition="Exists('..\packages\Microsoft.Bcl.Build.1.0.21\build\Microsoft.Bcl.Build.targets')" />

If you come across this error, pay extremely close attention to the contents of your project (`.csproj`) and manually verify the paths of all MSBuild includes.
