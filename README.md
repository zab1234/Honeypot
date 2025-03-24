# Honeypot Implementation Project/Guide
Creating a honeypot using tpot in a GCP compute instance. Goal of this project is to discover malicious traffic to my instance and visualize it to garner insights and gain hands on experience in implementing a honeypot and the current threat landscape. Feel free to use the following as a guide to implementing your own honeypot.

First I created a new GCP project labelled TPot and created a new e2-standard-2 VM instance on the Debian GNU/Linux 12 (bookworm) distro with a 128 GB disk named tpot-a.

![image](https://github.com/user-attachments/assets/874d38a4-b0f3-4648-996c-7a693287bfdf)

I then created a new firewall rule that allowed traffic from ANY IP to ANY port so that attackers could access the honypot and added my personal public ssh key to the instance so I could connect from my machine. 

![image](https://github.com/user-attachments/assets/94bde67f-ccaf-492b-bf31-feb794f7ec5b)

After connecting I update packages and add a sudo password. I then installed git and cloned the repository.

![image](https://github.com/user-attachments/assets/c93c118b-f461-4396-800f-543d2013fd31)

I then run the installer from the new tpotce directory and say yes to installing tpot and its dependencies. When prompted I elected to install in hive mode and later in the installation I setup web credentials to connect to the web UI later.

![image](https://github.com/user-attachments/assets/9916760b-1d38-4ecd-a5fb-423978072dea)
![image](https://github.com/user-attachments/assets/c1b45a74-d9e7-4fe3-9dfd-be4b4bc25240)
![image](https://github.com/user-attachments/assets/274f25c3-c554-4056-a47e-5689b19d11ad)

After completing the installation I rebooted the system as prompted and reconnected via ssh on port 64295.

![image](https://github.com/user-attachments/assets/05862b5f-b6a2-4014-9cd5-210f8d35feed)

Before starting the honeypot service I navigate to the compose directory and utilize the customizer.py script to choose the services I would like to enable. For now I will only be enabling the heralding honeypot service, which will capture credentials on a number of ports, along with the visualization services. For reference I will include a screenshot of the services that I've enabled.

![image](https://github.com/user-attachments/assets/aa0d1bb6-c5ad-45b2-b5a9-6104d9537752)
![image](https://github.com/user-attachments/assets/ab915238-f689-4e63-99ff-e4d2199d5f51)



