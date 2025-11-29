How to mitigate to Windows11 24H2 after

[Watch Demo Video](https://github.com/cobwebkanamachi/HBD8080A/blob/win11/HBD8080AWORKING.mp4)
I tried build this repo(original) on Visual Studio 2022 & win11 24h2.
So I met mainly two problems.
<PRE>
1) terminal invocation failed
fix path on Services\DumbTerminalService.cs:(bellow)
    private void TerminalTask() {
        try {
            //configure client
            if (pipeClient == null) {
                pipeClient = new Process();
                //                pipeClient.StartInfo.FileName = "F:\\dev\\HBD8080A\\DumbTerminal\\bin\\Debug\\net7.0\\DumbTerminal.exe";
                pipeClient.StartInfo.FileName = "C:\\Users\\user\\Downloads\\HBD8080A-master\\HBD8080A-master\\DumbTerminal\\bin\\Release\\net9.0\\DumbTerminal.exe";

2) .net version, windows version changed
win11-x64 -> win-x64
TargetFramework -> net9.0-windows10.0.26100
<Project Sdk="Microsoft.NET.Sdk">
  <PropertyGroup>
    <OutputType>WinExe</OutputType>
    <TargetFramework>net9.0-windows10.0.26100</TargetFramework>
    <TargetPlatformMinVersion>10.0.17763.0</TargetPlatformMinVersion>
    <RootNamespace>HBD8080A</RootNamespace>
    <ApplicationIcon>Assets/WindowIcon.ico</ApplicationIcon>
    <ApplicationManifest>app.manifest</ApplicationManifest>
    <Platforms>x86;x64;arm64</Platforms>
    <RuntimeIdentifier>win-x64</RuntimeIdentifier>
snip
</Pre>
Enjoy!
        
