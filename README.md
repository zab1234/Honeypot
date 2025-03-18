# Honeypot
Creating a honeypot using TPot in a GCP compute instance. Goals of this project is to discover malicious traffic to my instance and visualize it to garner insights.

First I created a new GCP project labelled TPot and created a new e2-standard-2 VM instance on the Debian GNU/Linux 11 (bullseye) distro with a 128 GB disk named tpot-a.

![image](https://github.com/user-attachments/assets/874d38a4-b0f3-4648-996c-7a693287bfdf)

I then created a new firewall rule that allowed traffic from ANY IP to ANY port so that attackers could access the honypot.

![image](https://github.com/user-attachments/assets/94bde67f-ccaf-492b-bf31-feb794f7ec5b)

Next I SSHed into the VM instance I created and updated the packages with apt.

![image](https://github.com/user-attachments/assets/6d1fdbff-1425-4ee0-9f8b-eb5f69ea5856)

For remote access through my personal machine I configured and tested public key ssh access

![image](https://github.com/user-attachments/assets/df77eb38-3679-415b-82fe-d2b89a7b9e67)
![image](https://github.com/user-attachments/assets/a0f5c2e0-58a8-4a8b-bff4-c41eb94390ac)
