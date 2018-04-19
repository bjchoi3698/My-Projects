What is Jenkins' Job?
It is something that we want Jenkins server to do, which will be anything. 
* Pull application codes from Git and compile them. 
* Deploy the code Ubuntu server
* Set the test after apps has been deployed
* utomate the dev and operation team such as updating VMware template
* etc

[Example: Create a job How much free space left on Jenkins server]

1. Go to Jenkins Web UI

2. Click "New Item" or "create new jobs" 

3. Fill in Item name : __FP-FreeSpace__

4. Choose "Freestyle Project" and click "OK"

5. Type Description if you need

6. In Freestyle Projects, 6 areas to be considered (General, Source Code Management, Build Triggers, Build Environment, Build, and Post-build Actions)

* General, 
  Check "Discard Old Builds" and set Max # of builds to keep to 10 (or whatever you want)
* Source Code Management,
  None to choose. Later we will cover others (Git and Subversion)  
* Build Triggers,  
* Build Environment,
* Build,
  Click __Add build step__ drop-down list, choose "Execute shell"
  In Command window, 
  ```
  df -h
  ```
* Post-build Actions


7. Click "SAVE" at the bottom of page

8. We are now at the Project page, Project 'FP-FreeSpace'

9. It is ready to build the first job to click "__Buid Now__"

10. After succssfully build, we can read the output at Console Output
```
Started by user Jenkins User
Building in workspace /var/lib/jenkins/workspace/FP-FreeSpace
[FP-FreeSpace] $ /bin/sh -xe /tmp/jenkins2115235906292823864.sh
+ df -h
Filesystem      Size  Used Avail Use% Mounted on
udev            493M   12K  492M   1% /dev
tmpfs           100M  380K  100M   1% /run
/dev/sda1        40G  2.9G   35G   8% /
none            4.0K     0  4.0K   0% /sys/fs/cgroup
none            5.0M     0  5.0M   0% /run/lock
none            497M     0  497M   0% /run/shm
none            100M     0  100M   0% /run/user
none            113G  109G  4.2G  97% /vagrant
Finished: SUCCESS
```



