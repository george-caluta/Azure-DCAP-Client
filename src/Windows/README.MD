# Build
1. Install Visual Studio 2017
1. Open `src/Windows/dcap_provider.vcxproj`
1. Save solution and Build in Debug X64 Configuration Mode
1. Switch Configuration Mode to Release X64 mode and then Build

<<<<<<< Updated upstream
# Build from Powershell
```powershell
cd c:\temp
git clone https://github.com/microsoft/Azure-DCAP-Client.git
cd Azure-DCAP-Client\src\Windows
#[Net.ServicePointManager]::SecurityProtocol = [Net.SecurityProtocolType]::Tls12 # Uncomment this line in case you get an error like: The request was aborted: Could not create SSL/TLS secure channel
.\get-prereqs.ps1
Invoke-WebRequest 'https://dist.nuget.org/win-x86-commandline/latest/nuget.exe' -OutFile .\nuget.exe
.\nuget.exe restore dcap_provider.vcxproj -PackagesDirectory packages
. "C:\Program Files (x86)\Microsoft Visual Studio\2017\BuildTools\MSBuild\15.0\Bin\MSBuild.exe" 'dcap_provider.vcxproj' /p:Configuration="Debug;Platform=x64"
. "C:\Program Files (x86)\Microsoft Visual Studio\2017\BuildTools\MSBuild\15.0\Bin\MSBuild.exe" 'dcap_provider.vcxproj' /p:Configuration="Release;Platform=x64"
```
> If you get an error like the script cannot be loaded because the execution of scripts is disabled on this system, run `Set-ExecutionPolicy bypass` and accept the changes.
=======
# Build from command line
```batch
cd src\Windows
build.bat Debug
build.bat Release
```
> If you get an error like the script cannot be loaded because the execution of scripts is disabled on this system, open a powershell console, run `Set-ExecutionPolicy bypass` and accept the changes.
>>>>>>> Stashed changes


# Packaging
Run `nuget pack` in this directory. If you need to bump the version number
or any other info, update the *.nuspec file.

Note: Your output package includes:
  libcurl.dll
  libeay32.dll
  libssh2.dll
  ssleay32.dll
  zlib.dll
These DLLs have the following external dependencies:
https://www.microsoft.com/en-us/download/details.aspx?id=30679#
https://www.microsoft.com/en-us/download/details.aspx?id=52685
