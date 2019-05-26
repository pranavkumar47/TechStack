# Install Jenkins 
# First Install OpenJDK.
- sudo yum Install -y java-1.8.0-openjdk-devel
# Downlaod the jenkins repo  
Jenkins repo is located at 
- wget -O /etc/yum.repos.d/jenkins.repo https://pkg.jenkins.io/redhat/jenkins.repo The Jenkins key for that repo is located at rpm --import https://pkg.jenkins.io/redhat/jenkins.io.key