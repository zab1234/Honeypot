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

To test this new configuration I install docker-compose and copy the new configuration file into ~/tpotce. By running docker-compose with the new configuration file I can see if there are any bugs. I discovered that heralding was unable to bind to port 25 due to it already being in use. For now I will simply be changing the config file to ignore port 25.

![image](https://github.com/user-attachments/assets/4624da89-61d1-49e5-a88c-f2a5e59b0d1c)
![image](https://github.com/user-attachments/assets/bfd3bcf8-1de1-4f66-92d7-20bbcac54847)
![image](https://github.com/user-attachments/assets/e7d7d444-85fd-43c2-847d-e2e12603b9ed)

Now I will try again to run tpot from this config file. I also ended up removing spiderfoot because it requires extra setup and I want to get things running first. I forgot to screenshot but the new configuration worked correctly. I then copied it to the docker-compose.yml file and rebooted the system before starting the tpot service. Connecting to the web UI and putting in my credentials I can now see the attack dashboards. As you can see traffic is already hitting my machine with multiple ssh login attempts originating from an IP in China.

![image](https://github.com/user-attachments/assets/d109cd14-4301-4097-afbd-4ada6fda7c48)
![image](https://github.com/user-attachments/assets/628a6db2-5f65-473a-9718-5b9fd17d9261)

Within minutes my machine was discovered and is being hammered by ssh authentication attempts from two hosts in China.

![image](https://github.com/user-attachments/assets/f28d9c30-c773-48ed-b81b-abac47f34d33)

In 24 hours I received over 12,000 authentication attempts to both ssh and telnet. Curiously, the most authentication attempts came from Poland, China and the United States. I expected more traffic originating from Russia, but this remained relatively low. I was also interested in the fact that The Netherlands made up the 4th most requests. I am interested in what percentage of this traffic is blackhat and how much could possibly be whitehat traffic attempting to help warn administrators of vulnerable systems.

![image](https://github.com/user-attachments/assets/ea0c7f6e-d422-48ee-bf22-e1428e48ada0)



