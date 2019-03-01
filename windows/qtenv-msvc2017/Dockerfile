FROM eckertj/vs-build-tools:latest

# Copy install script into container
COPY qtifwsilent.qs C:\\TEMP\\qtifwsilent.qs

# Download Qt installer 5.11.1
RUN powershell -NoProfile -ExecutionPolicy Bypass -Command \
    [Net.ServicePointManager]::SecurityProtocol = [Net.SecurityProtocolType]::Tls12; \
    $ErrorActionPreference = 'Stop'; \
    $Wc = New-Object System.Net.WebClient ; \
    $Wc.DownloadFile('https://download.qt.io/official_releases/qt/5.11/5.11.1/qt-opensource-windows-x86-5.11.1.exe', 'C:\\TEMP\\qt.exe') ; \
    Echo 'Downloaded qt-opensource-windows-x86-5.11.1.exe'

# Install Qt
RUN ["C:\\TEMP\\qt.exe", "--verbose", "--script C:\\TEMP\\qtifwsilent.qs"]

#Cleanup
RUN powershell -NoProfile -ExecutionPolicy Bypass -Command Remove-Item C:\\TEMP -Force -Recurse;

# Set Qt environment variable
ENV QTDIR "C:\\Qt\\5.11.1\\msvc2017_64"

# Default to PowerShell if no other command specified.
CMD ["powershell.exe", "-NoLogo", "-ExecutionPolicy", "Bypass"]