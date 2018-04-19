Use Git for source control. If need help, please visit "https://guides.github.com".

1. Install a few plugins unless they are already installed.
 * Open Jenkins UI
 * Click "Manage Jenkins"
 * Follow "Manage Plugins"
 * Check "__Installed__" tab. If not found, click "__Available__" tab and filter 'githug'b
 * Select "GitHub plugin" and click Download now and Install after restart
 
2. Before use Github, do a few things on Jenkins server such as installation of Git
```
# apt-get install git -y

# apt-get install apache2 -y

# chown jenkins /var/www/html -Rf

# visudo
...
Defaults:jenkins !requiretty,!lecture
jenkins ALL=NOPASSWD:/etc/init.d/apache2

ESC: wq!

```
(The last edit is only for environment that runs Apache and Jenkins on the same server. In real, it rarely occurs.)

3.
```
# su jenkins
$ cd ~
$ git clone git@github.com:devopslibrary/devopslibrary.github.io.git
Cloning into 'devopslibrary.github.io'...
The authenticity of host 'github.com (192.30.253.112)' can't be established.
RSA key fingerprint is 16:27:ac:a5:76:28:2d:36:63:1b:56:4d:eb:df:a6:48.
Are you sure you want to continue connecting (yes/no)? yes
Warning: Permanently added 'github.com,192.30.253.112' (RSA) to the list of known hosts.
Permission denied (publickey).
fatal: Could not read from remote repository.

Please make sure you have the correct access rights
and the repository exists.
```

4. Authentication
``` Creation of public key
$ ssh-keygen -t rsa -b 4096 -C "your-eamil_addr"
Generating public/private rsa key pair.
Enter file in which to save the key (/var/lib/jenkins/.ssh/id_rsa): /var/lib/jenkins/.ssh/github_rsa
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in /var/lib/jenkins/.ssh/github_rsa.
Your public key has been saved in /var/lib/jenkins/.ssh/github_rsa.pub.
The key fingerprint is:
d9:cb:a9:05:91:6e:d1:98:55:25:07:2c:9c:83:6d:80 your-email_addr
The key's randomart image is:
+--[ RSA 4096]----+
|       ..=.++oo  |
|      E .*B .o   |
|        *..o     |
|       . =       |
|        S .      |
|       . o o     |
|          =      |
|         o       |
|        .        |
+-----------------+

$ cat github_rsa.pub
ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAACAQDiha+kU/DihuSVEeXePEq+9SDccllg5Z6xW5l3T+qT2ujtXBqGwE0M6MjYQ7LH4HDxMXvNksCGmVyrTvvzTPkyFGglKsFL3Mv5IEkI+eiHT3X/0pz/oPGyICG900n7SBFtA5ix6n2aQxozrmWotRrSAXm22PqpQQZI7hpUEVjDMXByeGbGgvXSBkGr6n8wdCC1thd+bLh1XZElXUuGY5xWSG4RIKvmY4ihl21ubs73FJo1klIEiSeX9jKAGqZHbIh8QTZbGbM8EK6z1+EkQgKEJH0JkS+HpeyT3RSbWqrHi+Dg+410XH26t45OqNKXHM+pakNg5H/p0vUhv42oh4Rerf6EkmofAVQBcV8c34ahACd41sWYifB3Q7etm+SPgf165WXxZSt5Pj8FmjrJJYYfox16vaQtpA8nmQp8akG5jjlt7vKtOY6Gjqe9xf0A7hV1vLMw1DhTm/MGbCY7lvU73YDaQyyyMoCxr2Me7pIvBaKYrFkEQGNaq382Nyrbn3kMrF+xxZCgMQlFrl4LDO9EhpSkb4ORB9vpKQnOQHbYJ+ueI4cX1QZChmz2k1WDTNWqMK/vHk9PWpIFA3VRnOyORoE6z7vbXB4TqjBSCSjujMGkKEcLf/4tmQxGvwO0ve0DimP6aSI3pYMtG4q1qDiAJBIqloQl2qmmcLIBx8zx+w== your-email_addr
$
```

5. Goto Github and add newly created public key
 * Goto Settings
 * Click "SSH and GPG keys" on the left panel
 * Hit "New SSH key"
 * Use any name you like for Title and paste into "Key"

6. Goto Jenkins UI and create a new job as Freestyle

7. In the Source Code Management, Choose "Git" and paste the URL of git repository

Repository URL: https://github.com/bjchoi3698/devopslibrary.github.io.git

*Don't use* __use SSH__ It doesn't work at Repository URL any more.

8. Go to Build
   Choose "Execute Shell" from Add build step drop-down-list
   In Command,
   ```
   cp * /var/www/html/ -rf 
   sudo /etc/init.d/apache2 restart
   ```
   
9. Save the job
 
10. Build Now
 
11. View Console Output
```
Started by user Jenkins User
Building in workspace /var/lib/jenkins/workspace/FP-GitSourceControl
Cloning the remote Git repository
Cloning repository https://github.com/bjchoi3698/devopslibrary.github.io.git
 > git init /var/lib/jenkins/workspace/FP-GitSourceControl # timeout=10
Fetching upstream changes from https://github.com/bjchoi3698/devopslibrary.github.io.git
 > git --version # timeout=10
 > git fetch --tags --progress https://github.com/bjchoi3698/devopslibrary.github.io.git +refs/heads/*:refs/remotes/origin/*
 > git config remote.origin.url https://github.com/bjchoi3698/devopslibrary.github.io.git # timeout=10
 > git config --add remote.origin.fetch +refs/heads/*:refs/remotes/origin/* # timeout=10
 > git config remote.origin.url https://github.com/bjchoi3698/devopslibrary.github.io.git # timeout=10
Fetching upstream changes from https://github.com/bjchoi3698/devopslibrary.github.io.git
 > git fetch --tags --progress https://github.com/bjchoi3698/devopslibrary.github.io.git +refs/heads/*:refs/remotes/origin/*
 > git rev-parse refs/remotes/origin/master^{commit} # timeout=10
 > git rev-parse refs/remotes/origin/origin/master^{commit} # timeout=10
Checking out Revision 61c426d134aa9014b77ef4be033ad2517859c82f (refs/remotes/origin/master)
 > git config core.sparsecheckout # timeout=10
 > git checkout -f 61c426d134aa9014b77ef4be033ad2517859c82f
Commit message: "fixed"
First time build. Skipping changelog.
[FP-GitSourceControl] $ /bin/sh -xe /tmp/jenkins2070046377307242319.sh
+ cp CNAME DevOps.html Docker.html ELK.html Gemfile Gemfile.lock JUnit.xml Jenkins.html Linux.html PowerShell.html SaltStack.html Vagrant.html _config.yml _includes _layouts _posts _sass about.md bootstrap-salt.ps1 css devopsreport2016.pdf episode2-salt.zip episode3-jenkins.zip episode4-saltstates.zip episode5-jenkins.zip episode6-saltychocolate.zip episode7-docker.zip episode9-ELK.zip feed.xml googlecdce2281efbcaa92.html images index.html jenkinscloud.txt marketing newsletter.html sample.html sample_files scripts test.html vagrant /var/www/html/ -rf
+ sudo /etc/init.d/apache2 restart
 * Restarting web server apache2
AH00558: apache2: Could not reliably determine the server's fully qualified domain name, using 10.0.2.15. Set the 'ServerName' directive globally to suppress this message
   ...done.
Finished: SUCCESS
```


