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

6. 
