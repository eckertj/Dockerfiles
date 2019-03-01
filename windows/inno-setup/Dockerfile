FROM microsoft/windowsservercore

# Download inno setup
ADD http://files.jrsoftware.org/is/5/innosetup-5.6.1.exe C:\\TEMP\\innosetup.exe

# Install Inno Setup
RUN ["C:\\TEMP\\innosetup.exe", "/VERYSILENT"]

# Append Inno Setup to path variable
RUN setx PATH "%PATH%;C:\\Program Files (x86)\\Inno Setup 5"

#Cleanup
RUN powershell -NoProfile -ExecutionPolicy Bypass -Command Remove-Item C:\\TEMP -Force -Recurse;

# Default to PowerShell if no other command specified.
CMD ["powershell.exe", "-NoLogo", "-ExecutionPolicy", "Bypass"]