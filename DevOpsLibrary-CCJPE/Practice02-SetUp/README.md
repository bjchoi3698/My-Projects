Spin up a fresh Ubuntu 14.04 server on AWS

1. Login in the server
2. Get Jenkins key
```
# wget -q -O - http://pkg.jenkins-ci.org/debian/jenkins-ci.org.key | apt -key add -

# echo "deb http://pkg.jenkins-ci.org/debian binary/" | tee -a /etc/apt/sources.list
```
3. Install Java JDK 8
```
# add-apt-repository ppa:webupd8team/java -y

# apt-get update

# apt-get install oracle-java8-installer -y
```

4. Install Jenkins
```
# apt-get install jenkins -y
```
Installation of Jenkins is completed.

5. Connect Jenkins via http://_server-host_:8080


