<img width="1286" height="815" alt="image" src="https://github.com/user-attachments/assets/36cb3c1b-0ca1-4c7f-be3c-c3d79a4d0191" /># SplunkProject
A hands-on project for Splunk SIEM log analysis.


#🚀 Splunk Setup
##1. Splunk Enterprise(Server) Installation Process :
![Image Description](images/splunk_structure.png)


a)​ First, I downloaded the .deb version for my Parrot OS from the below website


“https://www.splunk.com/en_us/download/splunk-enterprise.html?locale=en_us” 


b)​ Then installed Splunk Enterprise. I installed it by running the command
```bash
sudo dpkg -i splunk-10.2.3-4d61cf8a5c0c-linux-amd64.deb
```
& also changed the ownership of the Splunk installation directory & everything
inside it by the command 
```bash
sudo chown -R tanvir13:tanvir13 /opt/splunk.
```
The commands are in the snapshot
