---
layout: post
title: SSH - Complete Guide, keys, passwords & connect
author: Abdul Bijur Vallarkodath
---
# SSH - Complete Guide, keys, passwords & connections

Why bother? The bother is that people are listening. Everyone from your prying neighbour, your ISP, your country and crackers and botnets are all listening to your traffic. Everytime you connect to a server online either through ftp, http, telnet etc. your login information and other information can be read by listeners since they arent encrypted. To overcome this, enter ftps, https and *ssh*.

SSH is a safe way of connecting, copying files and authenticating with a server online. You can generate your public key and let the server know your public key. By doing this, everytime you connect to the server, the server knows that the person connecting is you. You are the only person who can decrypt the public key with your private key that always only stays on your computer. 

## Generating SSH keys

On a linux/unix like machine (yes a mac too) run this

	ssh-keygen -t rsa -C "your_email@youremail.com"

This will prompt you for a passphrase. You could use one to be safe, so that if someone gets access to your private key, they cannot take advantage of it.

This will create two files 

	~/.ssh/id_rsa (your private key) 
and 
	~/.ssh/id_rsa.pub (your public key)

Keep your private key safe. The public key you can give away ;)

## Passwordless Authentication

For a server that you used to login into, use the keys above to enable passwordless authentication.

	$ cat ~/.ssh/id_rsa.pub 

This will output something similar to this
	ssh-rsa AAAAB3NzaC1yc2EAAAABIwAAAIEArkwv9X8eTVK4F7pMl 
	St45pWoiakFkZMw G9BjydOJPGH0RFNAy1QqIWBGWv7vS5K2tr+EEO+F8WL2Y 
	jK4ZkUoQgoi+n7DWQVOHsRijcS3LvtO+50Np4yjXYWJKh29JL6GHcp8o7
	+YKEyVUMB2CSDOP99eF9g5Q0d+1U2WVdB WQM=raman@ramantePC

It is one line in length. 

Login into your server the normal way and then copy this one line into .ssh/authorized_keys file using the following

	echo [your public_key] >> .ssh/authorized_keys

Thats it. Now log off and try ssh into your server again.

## ServerKeepAlive to maintain SSH Connections

Now that you are using ssh to connect yo your online server, you would have probably noticed how often ssh connections times out. This is because of one variable **ServerAliveInterval** in one of these files:

	/etc/sshd_config  or /etc/ssh/sshd_config

That's how often, in seconds, ssh will send a keepalive request to the other end of the connection. Now, I have found that at the servers, this value is usually set at 60. Setting your client machine to a value less than 60, like e.g. 45 is enough to make sure that there would be no idle timeout. 

This is relatively safe cos as long as your client computer is on, the connection is alive. The moment it goes to sleep or is shutdown, the connection is lost.

## ssh-agent, the true passwordless wonder

ssh-agent is considered a more safer way of connecting to servers as there are critics about the passwordless mechanism explained earlier. This is because of the vulnerability of having a file physically on your computer, that might get stolen etc. I haven't  delved into it much, but [this seems like a good link](http://mah.everybody.org/docs/ssh) for those who want to try it.
