🚀 A hands-on project for Splunk SIEM log analysis.


Total Splunk Structure
![Image Description](images/splunk_structure.png)

🛠️ Splunk Setup


1️⃣. Splunk Enterprise(Server) Installation Process :

a)​ First, I downloaded the .deb version for my Parrot OS from the website below


🔗 “https://www.splunk.com/en_us/download/splunk-enterprise.html?locale=en_us” 


b)​ Then installed Splunk Enterprise. I installed it by running the command
```bash
sudo dpkg -i splunk-10.2.3-4d61cf8a5c0c-linux-amd64.deb
```
& also changed the ownership of the Splunk installation directory & everything
inside it by the command. If there is any problem for the directory issue, then go to the root directory & apply it
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

2️⃣. Splunk Universal Forwarder Installation Process:

a) I downloaded the Splunk universal forwarder .msi version for my Windows Server 2019 from this link

🔗 “https://www.splunk.com/en_us/download/universal-forwarder.html”

b) Then I downloaded an Add-on from this link for my Windows Server 2019

🔗 “https://splunkbase.splunk.com/app/742”

& I downloaded the 7-zip from this website 

🔗 “https://www.7-zip.org/download.html” 

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

![Image Description](images/inputs.conf.png)

```bash
[WinEventLog://Application]
disabled = 0
index=wineventlog

[WinEventLog://Security]
disabled = 0
index=wineventlog

[WinEventLog://System]
disabled = 0
index=wineventlog

[WinEventLog://Microsoft-Windows-Sysmon/Operational]
disabled = 0
index=wineventlog
```

Or if the above don't work perfectly, we have to write more things in the inputs.conf file & in that case we have to create an extra limit.conf file

![Image Description](images/or_inputs.conf.png)

```bash
[WinEventLog://Application]
disabled = 0
index = wineventlog

[WinEventLog://Security]
disabled = 0
index = wineventlog

[WinEventLog://System]
disabled = 0
index = wineventlog
current_only = 1
start_from = newest

[WinEventLog://Microsoft-Windows-Sysmon/Operational]
disabled = 0
index = wineventlog
current_only = 1
start_from = newest
renderXml = 1
```

Here are the limits.conf file after writing extra in inputs.conf

![Image Description](images/limits.conf.png)

```bash
[thruput]
maxKBps = 0
```

This is deploymentclient.conf & where I typed the parrotOS(Splunk Enterprise(server)) IP(NAT) address (192.168.159.142)


![Image Description](images/deployment_client.conf.png)

```bash
[target-broker:deploymentServer]
targetUri = 192.168.159.142:8089
```

This is outputs.conf & where I typed the parrotOS(Splunk Enterprise(server)) IP(NAT) address(192.168.159.142)

![Image Description](images/outputs.conf.png)

```bash
[tcpout]
defaultGroup = default-autolb-group

[tcpout:default-autolb-group]
server = 192.168.159.142:9997

[tcpout-server://192.168.159.142:9997]
```

I tested the connection between the (Windows Server 2019)Splunk Forwarder and (Parrot OS)Splunk Enterprise through the command in cmd &


![Image Description](images/testing_connection_between splunk server&client.png)


powershell


![Image Description](images/checking_connection_via_powershell.png)


The command those are used to see the connection between the Splunk Enterprise (server) & splunk universal forwarder

i) going to the Splunk forwarder directory in the command

```bash
cd "C:\Program Files\SplunkUniversalForwarder\bin"
```
ii) to see the Splunk forwarder status in the command

```bash
.\splunk status
```

iii) to see the services of Splunk forwarder in PowerShell

```bash
Get-Service SplunkForwarder
```

iv) to test the connection in PowerShell

```bash
Test-NetConnection -ComputerName 192.168.159.142 -port 9997
```

v) to see the Splunk forward server in the command

```bash
.\splunk list forward-server
```
vi) Check what is happening on port 9997 in the Linux machine

![Image Description](images/Screenshot_202_06_09_22_04_04.png)

```bash
sudo netstat -tulnp | grep 9997
```

3️⃣. Sysmon Installation Process:

I downloaded the Sysmon from the link & extracted it

🔗 “https://learn.microsoft.com/en-us/sysinternals/downloads/sysmon” 

& sysmonconfig.xml file from the link, & placed it into the extracted Sysmon folder

🔗 “https://github.com/olafhartong/sysmon-modular/blob/master/sysmonconfig.xml”


I installed it with the

```bash
.\Sysmon64.exe -i .\sysmonconfig.xml
```

command & checked the sysmon with the command

```bash
Get-Service -Name Sysmon64
```

& it will run


![Image Description](images/check_sysmon.png)

![Image Description](images/sysmon_on_windows.png)

I also checked Sysmon through Splunk Enterprise

![Image Description](images/checking_sysmon_in_splunk_enterprise(linux_machine).png)

4️⃣. Showing Splunk Dashboard containing real-time logs from the Universal Forwarder Server.

![Image Description](images/showing_dashborad_on_linux_machine.png)


5️⃣. ART (Atomic Red Team) Installation process:

I turned off all of the windows' security system(virus & threat protection settings)

![Image Description](images/ART_installing_on_windows.png)


Then, I downloaded the zip file of atomic-red-team-master from the link

🔗 “https://github.com/redcanaryco/atomic-red-team”

& the zip file of invoke-atomicredteam-master from this link

🔗 “https://github.com/redcanaryco/invoke-atomicredteam” 

& Then I create a folder AtomicRedTeam in the local disk(C:)


![Image Description](images/installing_ART.png)


After the download, I unzipped those files & set the atomic-red-team-master folder & invoke-atomicredteam-master folder into the AtomicRedTeam folder.
Also sets the atomics folder into the AtomicRedTeam folder.

![Image Description](images/installing_ART1.png)


Then, I installed the AtomicRedTeam

i) 
```bash
powershell -exec bypass
```

ii)
```bash
Install-Module -Name invoke-atomicredteam,powershell-yaml -Scope CurrentUser
```

iii) 
```bash
Import-Module "C:\AtomicRedTeam\invoke-atomicredteam\Invoke-AtomicRedTeam.psd1" -Force
```

![Image Description](images/installing_ART_by_powershell.png)



Then I test some AtomicRedTeam Attack simulation with the command

i)

```bash
Invoke-AtomicTest T1016 -ShowDetailsBrief
```

ii)
```bash
Invoke-AtomicTest T1055 -ShowDetailsBrief
```

iii)
```bash
Invoke-AtomicTest T1570 -ShowDetailsBrief
```


iv)
```bash
Invoke-AtomicTest T1020 -ShowDetailsBrief
```

v)
```bash
Invoke-AtomicTest T1030 -ShowDetailsBrief
```
![Image Description](images/Screenshot_2026-06-07_17-31-25.png)
