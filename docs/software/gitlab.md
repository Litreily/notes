# Gitlab

## install deps

```bash
sudo apt update
sudo apt install ca-certificates curl openssh-server postfix
```

## install gitlab-ce

```bash
curl -s https://packages.gitlab.com/install/repositories/gitlab/gitlab-ce/script.deb.sh | sudo bash
sudo apt install gitlab-ce
```

## config

```bash
# edit below items if you need change
# - external_url # for domain name or static ip
# - letsencrypt # for https
sudo vim /etc/gitlab/gitlab.rb

# reconfigure, it's may need a few minutes, please be patient
sudo gitlab-ctl reconfigure
```

if you want to change the default path of git-data, such as change from `/var/opt/gitlib/git-data` to `/home/git/git-data`, you can set as below.

```bash
# need change to root user
sudo su
mkdir -p /home/git/git-data
chown -R git:git /home/git
cp -rf /var/opt/gitlab/git-data/* /home/git/git-data/
rm -rf /var/opt/gitlab/git-data/*

exit
sudo gitlab-ctl reconfigure
```

## access

open the web browser, and input the ip or domain.

1. set password for `root` user, which as admin
2. change account name from `root` to another
3. add SSH key for git clone/push repos

## reference

- [gitlab guick install](https://packages.gitlab.com/gitlab/gitlab-ce/install)
- [How To Install and Configure GitLab on Ubuntu 18.04](https://www.digitalocean.com/community/tutorials/how-to-install-and-configure-gitlab-on-ubuntu-18-04)
