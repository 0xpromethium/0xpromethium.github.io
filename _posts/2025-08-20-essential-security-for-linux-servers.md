---
layout: post
title: "Essential security for Linux servers"
date: 2025-08-20
---

<br>

This small post will go through the baseline on how to secure a freshly installed Debian based Linux distro. The aim of this approach is to create an acceptable security baseline while not adding extra layers of complexity.

```sh
# connect to the server
ssh root@[IP-adress]

```

set the correct timezone and enable network time sync and update the OS.

```sh
# set the time zone
dpkg-reconfigure tzdata

# enable network time sync
timedatectl set-ntp true

# update the repositories
apt update

# upgrade all the packages
apt upgrade

```


Connecting to the root account via ssh is highly discourged. Create an extra user for ssh.

```sh
# create the new user
useradd --create-home --shell /bin/bash [USERNAME]

# add the user to the sudoers
usermod -aG sudo [USERNAME]

# change the password
passwd [USERNAME]

```


Tweak the sshd config according to our security measures.

```sh
# edit /etc/ssh/sshd_config
Port 3392
PermitRootLogin no
PubkeyAuthentication yes
PasswordAuthentication no
AllowUsers [USERNAME]



#As an additional security measure, if you only log into the server from a specific IP address, you can lock down the openssh service even more by changing the last line to this

...
AllowUsers [USERNAME]@[IP-ADDRESS]

#Just make sure you have a static address or you won’t be able to login into the server if your IP changes.
```

A brief explaination of the changes above (in order):

    [x] - Change the default port to reduce some of the noise caused by bots trying to brute force our openssh server on port 22

    [x] - Disable login via ssh using the root account

    [x] - Enable public key authentication (we are going to generate a key pair to log into the server)

    [x] - Disable password authentication

    [x] - Permit login via ssh only to the newly created user


Now that the ssh service is secured, lets add our public key to the server to be able to login. With our public key ready we need to create the file structure, add the key to the authorized_keys file and assign the correct permissions:


```sh
# create the .ssh folder in the new user home
mkdir /home/[USERNAME]/.ssh

# restric access to it
chmod 700 /home/[USERNAME]/.ssh

# paste your public key into the authorized_keys file
nano /home/[USERNAME]/.ssh/authorized_keys

# lock down access to the key file
chmod 400 /home/[USERNAME]/.ssh/authorized_keys

# change ownership of the .ssh folder recursively
chown [USERNAME]:[USERNAME] -R /home/[USERNAME]/.ssh


```
Next step: We are enabling the firewall to block any unsolicited incoming traffic.


```sh

# open port 3392 on the firewall
ufw allow 3392/tcp

# enable the firewall at boot
ufw enable

# check the firewall status
ufw status

```


Reload the daemon to test tour config.


```sh

systemctl reload sshd

```

At this stage it’s good practice to fire up a new terminal window (while keeping the old ssh session open) to check that we are able to connect using our new user and public key:

```sh
ssh -p 3392 [USERNAME]@[IP-ADDRESS]

```

If the login fails we can still use the previous terminal session to debug the issue. If the connection works fine we can disconnect and go back to our old session.


In the next step we are going to install and configure two new packages.

The first one, called fail2ban, is a monitoring service that constantly scans the system logs and temporarily bans users via the system firewall if it detects suspicious activity (for instance too many failed ssh log in attempts from a specific IP address over a specified time range).

The second package, called ssmtp, is a simple smtp client that will be used by fail2ban to notify us via email.


```sh
apt install fail2ban ssmtp

```

To send emails from the server you can use any smtp relay you have access to.

```sh

# /etc/ssmtp/ssmtp.conf
root=postmaster
mailhub=mail
hostname=[HOSTNAME]
FromLineOverride=YES

# smtp server
mailhub=[SMTP]:[PORT]
UseSTARTTLS=yes
UseTLS=yes
AuthUser=[EMAIL]
AuthPass=[PASSWORD]


# edit /etc/ssmtp/revaliases
root:[EMAIL]:[SMTP]:[PORT]
postmaster:[EMAIL]:[SMTP]:[PORT]
[USERNAME]:[EMAIL]:[SMTP]:[PORT]


```

Fail2ban uses jail files to configure its behaviour so we need to copy the sample file to create our configuration:

```sh
cp /etc/fail2ban/jail.conf /etc/fail2ban/jail.local

```

Now that we have a new jail file we can tweak the configuration, it’s always a good idea to check the fail2ban man page for a detailed explaination of the settings:

```sh
# edit /etc/fail2ban/jail.local

# to email address
destemail = [EMAIL]

# from email address
sender = [EMAIL]

mta = sendmail

# tweak the action to get additional info in the email
action = %(action_mwl)s

# enable the sshd jail to monitor ssh connections
[sshd]
enabled = true

```

Finally we can start the fail2ban service:

```sh
systemctl start fail2ban

```
Last step is to setup automatic updates to avoid security breaches caused by vulnerabilities in out-of-date packages.

```sh
# /etc/apt/apt.conf.d/10periodic
APT::Periodic::Update-Package-Lists "1";
APT::Periodic::Download-Upgradeable-Packages "1";
APT::Periodic::AutocleanInterval "7";
APT::Periodic::Unattended-Upgrade "1";


#Then we enable the unattended upgrades:
# /etc/apt/apt.conf.d/50unattended-upgrades
Unattended-Upgrade::Allowed-Origins {
...
# comment-in the updates
"${distro_id}:${distro_codename}-updates";
...
}

# comment-in and enable automatic reboot
Unattended-Upgrade::Automatic-Reboot "true";

# comment-in the reboot time
Unattended-Upgrade::Automatic-Reboot-Time "02:00";

```




