<!-- README.md -->

# 🔓 ZLT X28 | ZLT X28 Modem Unlock

---

### ✨ ZLT X28 Modem Unlock & Custom Admin Panel
![](img/zlt.jpg)


### 📊 Device Specifications

| Model | Software Version |
|------------|----------------|
| ZLT X28    | 1.5.13         |

## 🚨 Serious warning
**If your modem version is different and you use this method, the modem panel will break.**

---
## Overview  
The ZLT X28 modem is based on a customized snapshot of [OpenWrt](https://www.google.com/search?q=OpenWrt). Unlocking this modem is straightforward but requires access to another modem (any brand or model) with an active internet connection.  

## Prerequisites  
- A second modem with internet access  
- LAN cable  
- Basic command-line knowledge  

## Step 1: Obtain `sessionId`  
Before anything else, you need to extract the ‍`sessionId`.  

Open your browser’s **Developer Tools**. The default shortcuts are:  

- **Windows/Linux**:  
  - `F12` → Opens the last used developer tools panel  


Inside Developer Tools, switch to the **Network** tab, select any request, and copy the `sessionId` value. Save it for later use.  

![](img/sessionId.png)

## Step 2: Enable WAN  
Connect a LAN cable from the internet-enabled modem to **Port 1** of the ZLT X28. This step is mandatory to activate **DMZ**, which cannot be enabled otherwise.  

Next, activate **WAN** on the ZLT X28 as shown below:  

![](img/enable-wan.png)

You can also enable WAN with this command and replacing `sessionId`.
```bash
curl 'https://192.168.70.1/cgi-bin/http.cgi' -X POST --data-raw '{"method":"POST","cmd":302,"LinkMode":"linkIP","IpVersion":"IPV4","IpMode":"dhcp","MTU":1500,"MRU":"","IpAddr4":"","Submask4":"","Gateway4":"","FirstDns4":"","SecDns4":"","NatEnable":"1","UserName":"","PassWd":"","priorityStrategy":"1","uisMode":"0","networkMode":"2","wifiMode2":"0","wifiMode5":"0","MacClone":"","vlanId":"","Dhcpv6Mode":"Yes","IpAddr6":"","IpAddr6Len":"","Gateway6":"","FirstDns6":"","SecDns6":"","wanRouter":"1","apnRouter0":"0","apnRouter1":"0","apnRouter2":"0","apnRouter3":"0","wifi2Router":"0","wifi5Router":"0","token":"cd55e4e9b9e941b0bf949db815d104d9","language":"EN","sessionId":"<YOUR_SESSION_ID>"}' -k

```

## Step 3: Enable Telnet  
Run the following command from your system’s terminal, replacing the placeholder `sessionId` with the one you retrieved earlier:  

```bash
curl 'https://192.168.70.1/cgi-bin/http.cgi' `
--data-raw '{"enabled":"1","ip":"192.168.70.1 ; telnetd -l /bin/ash","cmd":172,"method":"POST","success":true,"subcmd":6,"token":"5948b69147b3850eee5e7266188934c5","language":"EN","sessionId":"<YOUR_SESSION_ID>"}' -k
```

After this, Telnet will be enabled. Connect using:

```bash
telnet 192.168.70.1
```
## Step 4: Execute Unlock Script

Once inside Telnet, run the following command:
```bash
sh $(https://github.com/mahdigh782/Unlock-ZLT-X28/raw/refs/heads/main/x28)
```
The modem will restart after a few seconds. Once it powers back on, it will be unlocked.

