# User Account

## useradd

``` bash
# add user with root user
$ useradd USERNAME
# or add like that
$ useradd -m /home/USERNAME -s /bin/zsh USERNAME

# add password for new user
$ passwd USERNAME

# add user to sudoers
$ chmod u+w /etc/sudoers
$ vim /etc/sudoers
root    ALL=(ALL)  ALL
USERNAME ALL=(ALL)  ALL  # new line
```

``` bash
# login with new username and password
$ ssh USERNAME@HOSTIP

# change default shell of new user
$ chsh -s /bin/zsh
```

## chown

``` bash
# change the owner of directory or files
$ sudo chmod USERNAME DIRECTORY_OR_FILENAME
```

## chgrp

``` bash
# change the group of directory or files
$ sudo chgrp USERNAME DIRECTORY_OR_FILENAME
```

## userdel

``` bash
# with user in root
$ userdel USERNAME
# please make sure the files of USER already backup, then do the follow things
$ rm -rf /home/USERNAME
# remove USER from /etc/sudoers
```
