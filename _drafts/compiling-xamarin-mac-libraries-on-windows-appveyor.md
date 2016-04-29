# Compiling Xamarin Mac libraries on Windows / AppVeyor

1. Hack csproj or deploy custom msbuild targets
2. Compile

    C:\PROGRA~2\MSBuild\14.0\Bin\msbuild.exe MyCoolXamarinMacLibrary.sln /p:"ReferencePath=C:\Program Files (x86)\Reference Assemblies\Microsoft\Framework\Xamarin.Mac\v1.0" /p:"NoStdLib=true"

