# Nobus Cloud & Linux Challenge ☁️🐧

After completing my Azure cloud and Linux lab, I wanted to see if I could take what I had learned and apply it on another cloud platform.

This time, I worked with **Nobus**.

I wasn't trying to simply repeat the Azure lab. I wanted to test myself, see what I remembered, understand what worked differently, and troubleshoot things when they didn't go exactly as expected.

## What I Set Up

I created an Ubuntu cloud VM on Nobus and connected to it through SSH using MobaXterm.

The VM included:

- Ubuntu Server
- Virtual CPU and RAM
- Root/OS storage
- Additional storage
- Network connectivity
- Floating/public IP
- Nobus VPE/network

After connecting, I used the Linux terminal to inspect and manage the machine.

![Nobus VM Created](./Screenshot%202026-09-15%20153258.png)

![SSH Connection](./Screenshot%202026-09-15%20160040.png)

## Getting Familiar With the VM

I started by checking the resources and network information available on the server.

Some of the commands I used were:

lscpu
free -h
lsblk
df -h
ip addr
ip route

This helped me understand what the VM actually looked like from inside Linux instead of only looking at the Nobus dashboard.

I was able to check the CPU, RAM, disks, storage usage, IP addresses and routing information.

![Linux System and Network Checks](./Screenshot%202026-09-15%20163230.png)

## Linux Users and Permissions

I created a separate Linux user for the lab and gave the account sudo privileges.

sudo adduser cloudstudent
sudo usermod -aG sudo cloudstudent

I then switched into the new account and confirmed the active user.

I also created a small project directory and file:

mkdir ~/myproject
cd ~/myproject
touch test.txt
echo "This is my Cloud Student project." > test.txt

I experimented with file permissions using:

chmod 600 test.txt

This gave me more practical experience with Linux users, groups and permissions.

![Linux Users and Permissions](./Screenshot%202026-09-15%20164506.png)

## Installing Nginx

Next, I installed Nginx on the VM.

sudo apt update
sudo apt install nginx -y

I checked the service and tested it locally:

systemctl status nginx
curl localhost

I also accessed the Nginx welcome page through the VM's public IP to confirm that the web server could be reached externally.

This helped me connect the Linux side of the lab with networking and web-server concepts.

![Nginx Installation and Status](./Screenshot%202026-09-16%20125815.png)

## Adding Extra Storage

This was one of the parts that made me think a little more.

I created and attached an additional disk to the Nobus VM.

After identifying the new disk, I prepared it with the ext4 filesystem:


sudo mkfs.ext4 /dev/vdb

I then created a mount point and mounted the disk:

sudo mkdir /data
sudo mount /dev/vdb /data

I checked the available storage with:

df -h

I also created a test file inside the new storage:

sudo touch /data/test.txt

After rebooting the VM, I noticed that the /data mount was not automatically available again.

That was a useful lesson because it showed me that attaching a disk and mounting it are not the same thing as configuring it to automatically mount after every reboot.

I then used:

sudo blkid /dev/vdb


to identify the filesystem UUID and started working with /etc/fstab to understand persistent mounting.

![Nobus Vertical Scaling](./Screenshot%202026-09-16%20135326.png)

## VM Lifecycle

I also tested the VM lifecycle by working with the different states of the machine.

I checked the VM before and after:

Rebooting
Stopping
Starting

During this part, I checked things such as the IP addresses, storage and installed applications to see what remained available after the VM changed state.

This gave me a better understanding of the difference between simply rebooting a server and actually stopping/deallocating it.

## Vertical Scaling

I also tested vertical scaling on the Nobus VM.

Instead of creating another VM, I increased the resources of the existing machine.

After resizing, I checked the resources again from Linux using:

lscpu
free -h


This allowed me to see the change in CPU and RAM directly from the operating system.

The important thing I learned here is that vertical scaling means increasing the resources of an existing VM rather than creating a completely new machine.

What This Project Taught Me

This project was interesting because I had already worked with many of these concepts on Azure.

Nobus gave me the opportunity to find out whether I actually understood those concepts or whether I was simply following instructions.

Some things were familiar, while other parts worked differently.

I had to troubleshoot, look at the output from Linux commands and figure out what was happening.

The storage task was a good example. I initially expected the additional disk to remain available after reboot, but Linux showed me that I needed to understand persistent mounting and /etc/fstab.

That experience reminded me that cloud engineering isn't about memorising every command.

It's about understanding what you are trying to accomplish, knowing where to look when something doesn't work, and being able to adapt to a different environment.

Looking Back

I'm happy with how this project turned out.

When I started learning Cloud and DevOps, commands like lsblk, systemctl, chmod, mount and lscpu were completely new to me.

Now I'm getting more comfortable working inside a real cloud VM and understanding what is happening behind the cloud dashboard.

I was able to take what I learned from Azure and apply it to Nobus, while also dealing with situations that were different from my previous lab.

There is still a lot for me to learn, but being able to complete another cloud environment and troubleshoot along the way feels like real progress.

Azure tested me. Nobus tested what I learned from Azure. And I'm happy I got it done. 🚀☁️


Tools & Technologies
Nobus Cloud
Ubuntu Linux
MobaXterm
SSH
Nginx
Linux Users & Groups
Linux Permissions
Linux Storage
Networking
VM Lifecycle Management
Vertical Scaling
