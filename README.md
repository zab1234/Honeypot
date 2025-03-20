# Honeypot Implementation Project/Guide
Creating a honeypot using TPot in a GCP compute instance. Goal of this project is to discover malicious traffic to my instance and visualize it to garner insights and gain hands on experience in implementing a honeypot. Feel free to use the following as a guide to implementing your own honeypot!

First I created a new GCP project labelled TPot and created a new e2-standard-2 VM instance on the Debian GNU/Linux 11 (bullseye) distro with a 128 GB disk named tpot-a.

![image](https://github.com/user-attachments/assets/874d38a4-b0f3-4648-996c-7a693287bfdf)

I then created a new firewall rule that allowed traffic from ANY IP to ANY port so that attackers could access the honypot.

![image](https://github.com/user-attachments/assets/94bde67f-ccaf-492b-bf31-feb794f7ec5b)

Next I SSHed into the VM instance I created and updated the packages with apt.

![image](https://github.com/user-attachments/assets/6d1fdbff-1425-4ee0-9f8b-eb5f69ea5856)

For remote access through my personal machine I configured and tested public key ssh access

![image](https://github.com/user-attachments/assets/df77eb38-3679-415b-82fe-d2b89a7b9e67)
![image](https://github.com/user-attachments/assets/a0f5c2e0-58a8-4a8b-bff4-c41eb94390ac)

I then used apt to install git and cloned the tpot repo, which I will be using for hosting and managing my honeypot as well as aggregating and analyzing malicious traffic directed towards it. After downloading the repo I ran the install script before choosing the hive installation option when prompted. When prompted for a web username and password I entered credentials that will be used later in the project. Post install I rebooted the VM and re-connected via SSH over tcp/64295 as prompted.

![image](https://github.com/user-attachments/assets/46247a75-0675-4e7e-8201-aae5cee6d598)
![image](https://github.com/user-attachments/assets/3f82b7dd-8465-4f41-b940-05d1a97690bd)

After restarting the VM and connecting through the specififed port I double checked the status of tpot.

![image](https://github.com/user-attachments/assets/db3e08d7-5e39-468c-b8f5-5b2272248c69)

Connecting to the web page at https://<ip>:64297/ and entering the web credentials I established on setup I can view multiple different dashboards of traffic to my tpot.

![image](https://github.com/user-attachments/assets/23bdff74-29df-4370-ad32-c8e35b7e4e47)

With everything prepared I enabled the firewall rule I created earlier opening the honeypot to external traffic. 


