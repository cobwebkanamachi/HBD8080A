How to mitigate to Windows11 24H2 after

[Watch Demo Video](https://github.com/cobwebkanamachi/HBD8080A/blob/win11/HBD8080AWORKING.mp4)
<BR>
Now only patb and dumbterminal only tested.<BR>
<IMG SRC="https://github.com/cobwebkanamachi/HBD8080A/blob/win11/image1.jpeg"><BR>TINY BASIC WORKED</IMG><BR>

I tried build this repo(original) on Visual Studio 2022 & win11 24h2.<BR>
So I met mainly two problems.
```
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
3) IMSAI SCS worked! indeed
ShellPage.xaml.cs contains SCS invocation, but indeed that has blank definition on original source.
So I copy paloaltotinybasic invocation code from bellow of SCS, and path changed to scs.bin.
That changes are reflected to ShellPage.xaml.cs 2025/11/29 21:00 arround.
Change is mainly like this:
        var memory = File.ReadAllBytes("C:\\Users\\user\\Downloads\\HBD8080A-master\\HBD8080A-master\\HBD8080A\\Resources\\scs.bin");
You should change path of scs.bin.
First you should do to see SCS working, Power on then RUN then type something and ctrl-x.
If scs worked, you would see WHAT on screen.
Then test this.
ENTR 500
0 0A 30 44 FF FE/(enter)
DUMP 500
DUMP 501
:
DUMP 505
<BR><IMG SRC="https://github.com/cobwebkanamachi/HBD8080A/blob/win11/scsworked.jpg">SCS working</IMG><BR>
If same as you input displayed, you win!
:-) Greatly assisted bellow.
https://deramp.com/downloads/mfe_archive/010-S100%20Computers%20and%20Boards/00-Imsai/40-Imsai%20Software/1976%20Self%20Contained%20System/
and manual of SCS bellow.
https://deramp.com/downloads/mfe_archive/010-S100%20Computers%20and%20Boards/00-Imsai/40-Imsai%20Software/1976%20Self%20Contained%20System/12-Imsai%20SCS%20Manual%202002.pdf
```
Enjoy!
