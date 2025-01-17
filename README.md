Standardization:The /opt directory is used for optional software, keeping third-party apps separate from core system files.

    cd /opt

Isolation: Keeping Maven in /opt/maven contains all its files in one place, simplifying management.
Version Control: Install Maven in a specific directory to manage multiple versions easily.

    mkdir maven

Using chmod +x makes a file executable, allowing it to run as a program1. This is safer than chmod 777 as it only adds execute permissions without making the file writable by everyone.

    chmod 777 maven
    ls
    cd maven/

    wget https://dlcdn.apache.org/maven/maven-3/3.9.6/binaries/apache-maven-3.9.6-bin.tar.gz 
    ls
unzip the file
    tar -xvzf apache-maven-3.9.6-bin.tar.gz 
permission access:

    vi /etc/profile
copy and paste the below content:

    M2_HOME=/opt/maven/apache-maven-3.9.6 
    M2=$M2_HOME/bin 
    PATH=$PATH:$JAVA_HOME:$M2_HOME:$M2:$HOME/bin
    export PATH
• For Refreshing
  
    source /etc/profile
    echo $PATH
    echo $M2
list the java 

    apt list -a | grep OpenJDK
download java
                    
    apt-get install openjdk-11-jdk
java --version

   

        sudo wget -O /usr/share/keyrings/jenkins-keyring.asc \
          https://pkg.jenkins.io/debian/jenkins.io-2023.key
        echo "deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc]" \
          https://pkg.jenkins.io/debian binary/ | sudo tee \
          /etc/apt/sources.list.d/jenkins.list > /dev/null
        sudo apt-get update
        sudo apt-get install jenkins



------https://www.jenkins.io/doc/book/installing/linux/-------------

systemctl status jenkins

• Give sudo permission to jenkins user 
vi /etc/sudoers 
# and add below entry 
jenkins ALL (ALL) NOPASSWD: ALL



**************Docker - Installation on Jenkins
• Install Docker
apt update
apt install docker.io -y
docker --version
docker images
docker ps
• Add Jenkins User to Docker Group
sudo usermod -aG docker jenkins
• Restart Jenkins
sudo systemctl restart jenkins
sudo systemctl status jenkins
• Test Jenkins
http://<IP>:8080/

*************docker installation on [aws instance]docker-client ***********


• Install Docker
apt update
apt install docker.io -y
docker --version
docker images
docker ps
• Add ubuntu User to Docker Group
sudo usermod -aG docker ubuntu
sudo hostname docker-client


Jenkins - Pipeline Configuration
• Creating CI-CD pipeline in Jenkins using code from GitHub
• Creating WAR file using Maven
• Using Docker file for creating custom Docker Image for above WAR file
• Push Docker Image to Docker Hub
• Pull Docker image from Docker Hub
• Deploy Docker image to AWS Server

manage -->Available--->install all pipeline plugins--->[no need blue]--start without restart--->

Jenkins Plugins – Installation
• Maven Invoker
• Maven Integration
• SSH Agent
• Docker Pipeline
Amazon ECR
• All pipeline and GitHub (Custom)

• Blue - #0000FF
• White - #ffffff
manage available--->maven invoker-->start without restart
manage -->availale--->ssh agent
manage -->availale--->amazon ECR

**************Jenkins – Credentials Configuration -
go to manage jenkins--->global tool configuration--->
• Maven path
Maven=/opt/maven/apache-maven-3.9.6/

Manage jenkins---->manage credentials--->jenkins--->global credentials(unrestricted--->Add credntials-->
Creating Credentials for connecting GitHub
• King - YASEEN51449 and Password
. ID-git credentials

Creating Credentials for connecting Docker Hub
King - Secret text
password
ID- docker_hub

Creating Credentials to AWS Instance
• King-SSH Username with private key
. Username : ubuntu
  private key - Enter directly (paste pem file) 
  ID-aws_instance

Creating Credentials for Elastic Container Registry - ECR
King - SSH Username with private key
Username - ec2-user
private key - Enter directly (paste pem file)
ID- aws_instance
username:ubuntu
private kry -->enter directly
.pem 
copy &paste

ECR - Configuration
• Create ECR Repository on AWS
• Name - mahammadyaseen/docker-jenkins
• URI - 339713155907.dkr.ecr.ap-south-1.amazonaws.com/mahammadyseen/docker-jenkins

• Creating Credentials for Elastic Container Registry - ECR
• King - awscredentials
• Access key ID - From AWS Server  --AKIAU6GD3MNB47FTQUPA
• Secret Access key - From AWS Server --qDFfO4BzSLNO9os4iAUiZO7IF/FAIe1X73zfV+Ne
• ID - awscredentials

GitHub - Repository URL
• Repository URL -
https://github.com/YASEEN51449/Jenkins-Docker-Kubernetes-Project4-main.git
• Branch - main

------------------------------------------------------------------------------------

Jenkins – Pipeline Job

• Project Name - AWS-Docker-Project
• Stage - 1- Git Checkout - Create syntax for Git Hub
• Stage -2- Maven Clean Package
• Stage-3-Build Docker Image
• Stage-4-Push Image to Docker Hub
• Stage-5-Push Image in ECR
• Stage-5-Run Container on AWS Server
• Testing
http://<IP>:8080/
http://<IP>:8080/AWS-Docker-Amit-2/



nodel
stage(Git Checkout"){
git branch: main, credentialsid: git credentials, url: https://github.com/amit873/Jenkins-Docker-Kubernetes-Project4.git
stage(Maven Clean Package) {
def mavenHome tool name: "Maven", type: "maven"
det mavenCMD "S[mavenHome)/bin/mvn"
sh "$(mavenCMD) clean package"
stage(Build Docker Image'){
sh "docker build -t ameintu/docker-jenkins:$(env.BUILD ID)."
stage(Push Image to Docker Hub')(
withCredentials([string(credentialsId: docker hub, variable: docker hub)]) ( sh "docker login -u ameintu -p $(docker hub)"
1
sh "docker push ameintu/docker-jenkins:$(env.BUILD IDJ
stage(Push Image in ECR){
ECRURL https://233402516001.dkr.ecr.us-east-1.amazonaws.com
ECRRED ecr:us-east-1:awscredentials docker.withRegistry("$(ECRURL)", "$[ECRRED]")[
docker.image("ameintu/docker-jenkins:$(env.BUILD ID)").push()
1
stage Run Container on AWS Server){
def dockerRun "docker run -d-p8080:8080-name myapp-$(env.BUILD_ID) ameintu/docker-jenkins:S(env.BUILD ID) sshagent(['aws instance']) (
sh "ssh -o StrictHostKevChecking no ubuntu 172.31.31.83 5(dockerRun)"






Webhook - Configuration
• Adding Webhook to GitHub Repository Payload URL - http://<IP>:8080/github-webhook/
Enable 'GitHub hook trigger for GITScm polling' in jenkins Project
• Testing
• Clone code in local
https://github.com/amit873/Jenkins-Docker-Kubernetes-Project4.git
• Change in index.html
Jenkins-Docker-Kubernetes-Project4/src/main/webapp/index.html
• Commit and push the changes in Git Hub
• Test the URL
http://<IP>:8080/
http://<IP>:8080/AWS-Docker-Amit-2/



-------------------------------------****************************------------------------------------------------
****1.create user natasha,hari,sara set a common password algebra and hari and natasha are in wheel group.****
 


**1. Switch to the root user**

       sudo su -

sudo su -: This command switches you to the root user, giving you administrative privileges to perform system-wide changes.

**2. Create users and set passwords**

    useradd hary
    passwd hary
    useradd natasha
    passwd natasha
    useradd sara
    passwd sara

useradd hary: Creates a new user named hary.
passwd hary: Sets the password for the user hary. You will be prompted to enter the password (in this case, “algebra”).
useradd natasha: Creates a new user named natasha.
passwd natasha: Sets the password for the user natasha.
useradd sara: Creates a new user named sara.
passwd sara: Sets the password for the user sara.

**3. Add users to the wheel group**
            
    usermod -G wheel hary
    usermod -G wheel natasha

usermod -G wheel hary: Adds the user hary to the wheel group. The wheel group typically has administrative privileges.
usermod -G wheel natasha: Adds the user natasha to the wheel group.

**4. Verify the users in the wheel group**

    cat /etc/group | grep -i wheel

cat /etc/group: Displays the contents of the /etc/group file, which lists all the groups and their members.
grep -i wheel: Filters the output to show only the lines containing “wheel”, ignoring case sensitivity.

Explanation of the output
wheel:x:10:ec2-user,hary,natasha

wheel: The name of the group.
x: Indicates that the group has a password (usually not used in modern systems).
10: The Group ID (GID) for the wheel group.
ec2-user,hary,natasha: The list of users who are members of the wheel group.

    Summary
    sudo su -: Switch to root user.
    useradd: Create new users.    
    passwd: Set passwords for users.
    usermod -G wheel: Add users to the wheel group.
    cat /etc/group | grep -i wheel: Verify users in the wheel group.
