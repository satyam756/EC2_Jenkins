# Jenkins installation on ec2 ubuntu machine

## Signin to AWS account using ROOT email
[SignIN](https://ap-south-1.console.aws.amazon.com/console/home?region=ap-south-1)

## Launch an EC2 Instance of ubuntu machine

>   Services > EC2 > Launch instance

>   give name of the instance ex: JenkinsInstance > Ubuntu(AMI) > t2.micro(free tier) 

>   Network settings - select: Allow HTTPS traffic from the internet, Allow HTTP traffic from the internet > Launch instance

>   wait until instance Status check is 2/2 checks passed

> EC2 Instance Connect

## updating the system and installing jenkins

>   This is the Debian package repository of Jenkins to automate installation and upgrade. To use this repository, first add the key to your system 

```
sudo wget -O /usr/share/keyrings/jenkins-keyring.asc \
  https://pkg.jenkins.io/debian/jenkins.io-2023.key

```

>   Then add a Jenkins apt repository entry:

```
echo "deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc]" \
  https://pkg.jenkins.io/debian binary/ | sudo tee \
  /etc/apt/sources.list.d/jenkins.list > /dev/null
```

>   Update your local package index, then finally install Jenkins

```
sudo apt-get update
sudo apt-get install jenkins -y

```

>   Jenkins requires java to be installed..

```
sudo apt install fontconfig openjdk-17-jre -y
java -version

```

>   enable/start and check the service status of jenkins

```

sudo systemctl enable jenkins
sudo systemctl start jenkins
sudo systemctl status jenkins | grep active

```

## jenkins runs on port 8080

>   update the inbound rule for the instance to allow tcp from anywhere on port 8080

>   instance > security > security groups > Edit inbound rule > Add rule > save rule

>   copy the public ipv4 address ex: ipv4_address:8080

>   sudo cat /var/lib/jenkins/secrets/initialAdminPassword

>  install suggested plugins / select plugin to install

>   setup the initial user ⭐

### References

>   [Reference 1](https://www.jenkins.io/doc/book/installing/linux/#debianubuntu)

>   [Reference 2](https://pkg.jenkins.io/debian-stable/)