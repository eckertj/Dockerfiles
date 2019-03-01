FROM openjdk:13-jdk-windowsservercore

# Download maven
ADD https://www-us.apache.org/dist/maven/maven-3/3.6.0/binaries/apache-maven-3.6.0-bin.zip C:\\TEMP\\maven.zip

# Install maven
RUN jar -xvf  C:\\TEMP\\maven.zip

# Set env variables
RUN setx MAVEN_HOME "C:\\apache-maven-3.6.0"
RUN setx PATH '%PATH%;%MAVEN_HOME%\\bin'

# Default to PowerShell if no other command specified.
ENTRYPOINT [ "cmd.exe" ]