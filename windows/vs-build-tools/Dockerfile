FROM microsoft/windowsservercore

# Download useful tools to C:\tools
ADD https://dist.nuget.org/win-x86-commandline/v4.1.0/nuget.exe C:\\tools\\nuget.exe

# Download the Build Tools bootstrapper outside of the PATH.
ADD https://aka.ms/vs/15/release/vs_buildtools.exe C:\\TEMP\\vs_buildtools.exe

# Install build tools 
RUN C:\\TEMP\\vs_buildtools.exe --wait --quiet --norestart --nocache --installPath C:\BuildTools \

#    MSBuild Components
    --add Microsoft.Component.MSBuild \
    --add Microsoft.VisualStudio.Component.CoreBuildTools \
    --add Microsoft.VisualStudio.Component.Roslyn.Compiler \

#   VC++ Components
    --add Microsoft.VisualStudio.Component.VC.CoreBuildTools \
    --add Microsoft.VisualStudio.Component.VC.Redist.14.Latest \
    --add Microsoft.VisualStudio.Component.Windows10SDK \
    --add Microsoft.VisualStudio.Component.Static.Analysis.Tools \
    --add Microsoft.VisualStudio.Component.VC.CMake.Project \
    --add Microsoft.VisualStudio.Component.VC.Tools.x86.x64 \
#   UCRT
    --add Microsoft.Component.VC.Runtime.UCRTSDK \
    --add Microsoft.VisualStudio.ComponentGroup.NativeDesktop.Win81 \

#   .Net
    --add Microsoft.Net.Component.4.5.TargetingPack \
    --add Microsoft.VisualStudio.Component.PortableLibrary \
    --add Microsoft.Net.Component.4.6.SDK \
    --add Microsoft.Net.Component.4.6.TargetingPack \
    --add Microsoft.Net.ComponentGroup.TargetingPacks.Common \

#   VC++ 2015
    --add Microsoft.VisualStudio.Component.VC.140 \

#    ARM | Arm64
    --add Microsoft.VisualStudio.Component.VC.Tools.ARM \
    --add Microsoft.VisualStudio.Component.VC.Tools.ARM64 \

#   Windows SDK
    --add Microsoft.VisualStudio.Component.Windows10SDK.16299.Desktop \
    --add Microsoft.VisualStudio.Component.Windows81SDK \
    --add Microsoft.VisualStudio.Component.Windows10SDK.15063.Desktop \
    --add Microsoft.VisualStudio.Component.Windows10SDK.16299.Desktop.arm \
    || IF "%ERRORLEVEL%"=="3010" EXIT 0

# Cleanup
RUN powershell -NoProfile -ExecutionPolicy Bypass -Command Remove-Item C:\\TEMP -Force -Recurse;

# Start developer command prompt with any other commands specified.
ENTRYPOINT C:\BuildTools\Common7\Tools\VsDevCmd.bat &&

# Default to PowerShell if no other command specified.
CMD ["powershell.exe", "-NoLogo", "-ExecutionPolicy", "Bypass"]