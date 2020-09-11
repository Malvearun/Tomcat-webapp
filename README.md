# Tomcat-webapp


#### Launch an EC2 Instance and Configure.

•	Select the correct region. 

•	AWS Console &rarr; Services &rarr; EC2 &rarr; Launch Instance > 
1.	Choose AMI ‘Linux’
2.	Choose the Instance type as `depending upon requirement` 
3.	Configuration Instance Details:
a.	Auto-assign Public IP: `Enable`
4.	Add Storage: default
5.	Tags: Default
6.	Review and launch.
7.	Create a new key pair – `my-keypair` and `Download key pair`
8.	It will take few minutes to initialize the instance.
•	Select the instance and click on connect and select connection method has `EC2 instance connect` and click `connect`.
•	To run all admin commands in this CLI.



### Tomcat installation for webapp

#### Java JDK installation on EC2 instance.

run `sudo yum list | grep openjdk` to filter the correct version for java installation.

run `sudo yum install java-1.8.0-openjdk.x86_64`

run `cd ~` change to home dir

run `ls -la` to view the file in home dir

run `file $(which java)` check where java in located with an output
output: /usr/bin /java symbolic link `/etc/alternatives/java`

run `file /etc/alternatives/java`

run `sudo vim .bash_profile`

-----------
 #Java env variable setup

JAVA_HOME="/usr/lib/jvm/java-1.8.0-openjdk-1.8.0.252.b09-2.amzn2.0.1. x86_64/jre/"

PATH=$JAVA_HOME/bin:$PATH

export PATH </code>

---------

run `source .bash_profile`

run `echo $PATH`

run `echo $JAVA_HOME`


•	By default, newer versions of Tomcat restrict access to the Manager and 

Host Manager apps to connections coming from the server itself. Since we are 

installing on a remote machine, you will probably want to remove or alter this 

restriction. To change the IP address restrictions on these, 

open the appropriate context.xml files.


run $ sudo vim $TOMCAT_HOME/webapps/manager/META-INF/context.xml

run $ sudo vim $TOMCAT_HOME/webapps/host-manager/META-INF/context.xml



Inside, comment out the IP address restriction to allow connections from anywhere. 

Alternatively, if you would like to allow access only to connections coming from 

your own IP address, you can add your public IP address to the list:

`<Context antiResourceLocking="false" privileged="true" >

<!--<Valve className="org.apache.catalina.valves.RemoteAddrValve"

allow="127\.\d+\.\d+\.\d+|::1|0:0:0:0:0:0:0:1" />-->

</Context>`

•	Role addition in tomcat-users.xml

run `vi conf/tomcat-users.xml`

`<role rolename="admin-gui"/> <user username="admin" password="password" roles="manager-gui,manager-status,admin-gui"/>`

•	To restart the tomcat service follow below two commands:
run ` ./shutdown.sh`
run `./startup.sh`
run `ps -ef | grep tomcat`

•	 From AWS console, copy the public DNS ip address and paste in browser `ec2-35-174-209-223.compute-1.amazonaws.com:8080`

•	 Click on `Manager app` and login to Tomcat Web Application Manager with user name and password has mentiond above.












