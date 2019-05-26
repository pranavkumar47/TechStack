# Install Jenkins
## Check SELINUX is disabled or not 
    Step 1 nano /etc/sysconfig/selinux
    Make sure the file has this configurations
    SELINUX=disabled
    SELINUXTYPE=targeted
    Then restart the system
    Step 2
    iptables -A INPUT -m state --state NEW -p tcp --dport 8080 -j ACCEPT
    Step 3
    sudo service iptables save
    For Cent OS 7
    step 1
    firewall-cmd --zone=public --permanent --add-port=8080/tcp
    Step 2
    firewall-cmd --reload
## Check the ports are open or not 
**If you have a firewall installed, you must add Jenkins as an exception. You must change YOURPORT in the script below to the port you want to use. Port 8080 is the most common.**

    firewall-cmd --permanent --new-service=jenkins
    firewall-cmd --permanent --service=jenkins --set-short="Jenkins Service Ports"
    firewall-cmd --permanent --service=jenkins --set-description="Jenkins service firewalld port exceptions"
    firewall-cmd --permanent --service=jenkins --add-port=YOURPORT/tcp
    firewall-cmd --permanent --add-service=jenkins
    firewall-cmd --zone=public --add-service=http --permanent
    firewall-cmd --reload

### To Enable all the incoming ports for a service
    You can also open the required ports for a service by using the –add-service option. To permit access by HTTP clients for the public zone: 
    -- firewall-cmd --zone=public --add-service=http
    success
    To list services that are allowed for the public zone: 
    -- firewall-cmd --zone=work --list-services
    dhcpv6-client http ssh
    Using this command only changes the Runtime configuration and does not update the configuration files. The following sequence of commands shows that configuration changes made in Runtime configuration mode are lost when the firewalld service is restarted:
    -- systemctl restart firewalld
    -- firewall-cmd --zone=work --list-services
    dhcpv6-client ssh
    To make changes permanent, use the –permanent option. Example:
    -- firewall-cmd --permanent --zone=public --add-service=http
    success
    Changes made in Permanent configuration mode are not implemented immediately. Example:
    -- firewall-cmd --zone=work --list-services
    dhcpv6-client ssh
    However, changes made in a Permanent configuration are written to configuration files. Restarting the firewalld service reads the configuration files and implements the changes.
    Example:
    -- systemctl restart firewalld
### Allow traffic on an incoming port
    This command to check ports are open and listening 
    netstat -anl | grep 8080
    The command below will open the port 2222 effective immediately, but will not persist across reboots:
    -- firewall-cmd --add-port=[YOUR PORT]/tcp
    For example, to open TCP port 2222 :
    -- firewall-cmd --add-port=2222/tcp
    The following command will create a persistent rule, but will not be put into effect immediately:
    -- firewall-cmd --permanent --add-port=[YOUR PORT]/tcp
    For Example, to open TCP port 2222 :
    -- firewall-cmd --permanent --add-port=2222/tcp
    To list the open ports, use the command :
    -- firewall-cmd –-list-ports 2222/tcp
    -- firewall-cmd --zone=public --permanent --add-port=8080/tcp
# Install OpenJDK.
    - sudo yum Install -y java-1.8.0-openjdk-devel
# Download the jenkins repo  
    Jenkins repo is located at 
    -  sudo wget -O /etc/yum.repos.d/jenkins.repo https://pkg.jenkins.io/redhat/jenkins.repo 
    The Jenkins key for that repo is located at 
    - rpm --import https://pkg.jenkins.io/redhat/jenkins.io.key
# Install jenkins package 
    - sudo yum install -y jenkins  


# Linux (jenkins doc)
## Debian/Ubuntu
    On Debian-based distributions, such as Ubuntu, you can install Jenkins through apt.

    Recent versions are available in an apt repository. Older but stable LTS versions are in this apt repository.

    wget -q -O - https://pkg.jenkins.io/debian/jenkins.io.key | sudo apt-key add -
    sudo sh -c 'echo deb https://pkg.jenkins.io/debian-stable binary/ > /etc/apt/sources.list.d/jenkins.list'
    sudo apt-get update
    sudo apt-get install jenkins
    This package installation will:

    Setup Jenkins as a daemon launched on start. See /etc/init.d/jenkins for more details.

    Create a ‘jenkins’ user to run this service.

    Direct console log output to the file /var/log/jenkins/jenkins.log. Check this file if you are troubleshooting Jenkins.

    Populate /etc/default/jenkins with configuration parameters for the launch, e.g JENKINS_HOME

    Set Jenkins to listen on port 8080. Access this port with your browser to start configuration.

    If your /etc/init.d/jenkins file fails to start Jenkins, edit the /etc/default/jenkins to replace the line ----HTTP_PORT=8080---- with ----HTTP_PORT=8081---- Here, "8081" was chosen but you can put another port available.

# Post installation setup
Unlocking Jenkins
When you first access a new Jenkins instance, you are asked to unlock it using an automatically-generated password.

Browse to http://localhost(OR)IP:8080 (or whichever port you configured for Jenkins when installing it) and wait until the Unlock Jenkins page appears.

From the Jenkins console log output, copy the automatically-generated alphanumeric password (between the 2 sets of asterisks).

## Creating the first administrator user
Finally, after customizing Jenkins with plugins, Jenkins asks you to create your first administrator user.

When the Create First Admin User page appears, specify the details for your administrator user in the respective fields and click Save and Finish.
