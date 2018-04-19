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
# cd ~
# git clone git@github.com:devopslibrary/devopslibrary.github.io.git

```
