🚀 A hands-on project for Splunk SIEM log analysis.


#🛠️ Splunk Setup


Total Splunk Structure
![Image Description](images/splunk_structure.png)

#🛠️ Splunk Setup


1. Splunk Enterprise(Server) Installation Process :

a)​ First, I downloaded the .deb version for my Parrot OS from the website below


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
![Image Description](images/installing_splunk_on_linux.png)


c) Then I went to the directory by running the command
```bash
cd /opt/splunk/bin
```

& started it by running the command
```bash
./splunk start
```
![Image Description](images/starting_splunk_enterprise_on_linux.png)

d) Then I copied the link address
```bash
http://parrot:8080
```
that I got from the CLI and pasted it into the Google browser.Then the address was sent to the Splunk Enterprise server interface.

![Image Description](images/splunk_on_linux_machine.png)

e) Then I typed the name & password & this interface was shown in the background.

![Image Description](images/splunk_enterprise_dashboard_on_linux.png)

2. Splunk Universal Forwarder Installation Process:

a) I downloaded the Splunk universal forwarder .msi version for my Windows Server 2019 from this link

“https://www.splunk.com/en_us/download/universal-forwarder.html”

b) Then I downloaded an Add-on from this link for my Windows Server 2019

“https://splunkbase.splunk.com/app/742”

& I downloaded the 7-zip from this website 

“https://www.7-zip.org/download.html” 

to extract the Add-on file

c) Then I installed the Splunk forwarder. There are some snapshots from the time of installation of the forwarder. I marked the local system in the snapshot

![Image Description](images/installing_splunk_universal_forwarder_on_windows.png)

Then I typed the username & password

![Image Description](images/installing_splunk_universal_forwarder_on_windows1.png)

Then I typed the IP address of Windows Server 2019(192.168.159.138) & default port 8089 in the Deployment Server

![Image Description](images/installing_splunk_universal_forwarder_on_windows2.png)

& I typed the same IP address & default port 9997 in the Receiving Indexer

![Image Description](images/Screenshot_2026-06-06_20-13-54.png)

This is the location of Splunk Universal Forwarder on my Windows machine.

![Image Description](images/Screenshot_2026-06-06_20-14-13.png)

This is the Splunk Add-on & I extracted it with 7-Zip twice & finally, I got the Splunk_TA_windows-10.0.1 folder

![Image Description](images/Screenshot_2026-06-06_20-14-32.png)


This is the inside of the Splunk_TA_windows-10.0.1 folder

![Image Description](images/Screenshot_2026-06-06_20-15-02.png)

Here, I placed the Splunk_TA_windows-10.0.1 folder into the Splunk Forwarder

![Image Description](images/Screenshot_2026-06-06_20-15-19.png)

This is an inputs.conf


