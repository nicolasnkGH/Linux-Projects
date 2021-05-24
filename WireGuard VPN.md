# WireGuard VPN 

I created my own personal VPN in order to make my home internet more secure and so I would be able to access my home network from anywhere. For this, 
I used the WireGuard VPN tunnel.

First, I created a dynamic DNS hostname on the website ```freedns.afraid.org```.

The next step was to install and set up ddclient:

```sudo apt install ddclient```

Just keep pressing enter until the installation is finished.

Set up which address ddclient needs to update:

```sudo nano /etc/ddclient.conf```

Delete all of the lines in the file and substitute with the following:
```
daemon=5m
timeout=10
protocol=freedns
#use=if, if=eth0
use=web, web=dynamicdns.park-your-domain.com/getip
ssl=yes
server=freedns.afraid.org (or whichever service you used)
login=YOUR_LOGIN_INFORMATION
password='YOUR_PASSWORD_IN_QUOTATION'
YOUR_DOMAIN_HERE
```
Save and close the file!

Restart ddclient to make the new configurations work:

```sudo systemctl restart ddclient```

Here you can check for the status of the server:

```sudo systemctl status ddclient```

Make ddclient starts automatically every time the computer (Raspberry Pi) restarts or it is powered on:

```sudo systemctl enable ddclient```

In order to have your IP address updated automatically on FreeDNS, follow the steps below:
    
    - Go to the tab Dynamic DNS
    - Mark the option for dynamic updates for your domain
        * This is step is necessary in order to make your IP address to be updated every time your IP changes.
    - Choose for of authentication that most suits you. If not sure on which one to use, just choose the recommended option
      and follow the steps. 
        * Freedns provides tips and guides on how to proceed with configuration.

Make sure to set up port forwarding on your router for the Raspberry pi:

    Device: Raspberry Pi's hostname or IP
    Protocol: UDP
    Port range: 51820-51820
    Outgoing port: 51820
    Permit Internet access: yes

# WireGuard VPN installation

```sudo apt install wireguard```

Set up host name as the same as the dynamic DNS domain created on freedns.afraid.org.
Set any client name you would like, and for the DNS, use your personal preference - I used 1.1.1.1

It is done!

For every user or device, you need to set up a new client with different keys. To do that, just re-run the script and choose the option add new client. 
The script is also used to manage existent clients.

```wget https://git.io/wireguard -O wireguard-install.sh && sudo bash wireguard-install.sh```

In order to have the VPN working on other devices or computers, the WireGuard application is necessary. For mobile devices, go to the app store and 
download WireGuard app. While creating new clients, a QR code will be outputted on the terminal window. Simply scan the QR code with the WireGuard app and you should be able to connect with no issues.

To have WireGuard set up on a computer, you also need to download the Wireguard software. Although, the process is a little bit more extensive. You need to copy the ```".conf"``` files to the desired computer. 

This method works for Windows and IOS as well!

Move the configuration files to the home directory. Go to the terminal and type:

```sudo su```
```cp /root/*.conf /home/YOUR_SERVER_NAME```

Now, copy the ```.conf``` files named for the desired computer into a USB driver:

Open a new directory and then open the Windows Powershell in that directory  ( or other application you would like to use instead)

    - Connect to the Raspberry py from there using sftp instead ssh.
    
    sftp ubuntu@YOUR_IP_HERE
    
    To copy the files to the desire directory, use the command
    
```sftp get *.conf ```

Download the WireGuard software and import the desired file and it should work.

This method worked great for me and I am able to access the Internet using my home IP from anywhere. I have access to my router and servers while using public networks. I also created a client for a friend in Brazil and he was able to connect and have access to my home internet from there.

# IF FILES CANNOT BE FOUND

If for some reason you cannot find the files using the methods above, use the commands below to manually find the .conf files and copy the private keys configuration.

    - Knowing where the Wireguard stored the file, normally at /root/NAME OF THE FILE.conf
      * type on the terminal:
        
        ```sudo su```
        
      This will take you to the root access
      
      * Next, type:
      
        ```cat /root/NAME_OF_THE_FILE.conf```
        
       The output should be the configuration. It should look something like this:
```       
       [Interface]
Address = 10.7.0.6/24
DNS = 1.1.1.1, 1.0.0.1
PrivateKey = SE877pghe9Kdmeizj9xAeUADo8rFttXjn69IIY0KWF=

[Peer]
PublicKey = U890bxhbpXOJIk1xp/Xra3FS+vRK20XPnZ5aYH3PQk=
PresharedKey = bNsfRnUMCuywSHPZkNj/C5n/BSplzqMWYvCcQkaKos=
AllowedIPs = 0.0.0.0/0, ::/0
Endpoint = RaspberryVPN.crabdance.com:51820
PersistentKeepalive = 25
root@ubuntu:/home/ubuntu# cat /root/Nicolas_Dell.conf
[Interface]
Address = 10.0.0.4/24
DNS = 1.1.1.1, 1.0.0.1
PrivateKey = oEePGPy3ufjvmtMUdGm1RxitUtnEvcz23LEOOLGJ5X=
```

Go to Wireguard app and choose the option to add the keys manually and past it there.


# IF THE DDCLIENT DO NOT AUTOMATICALLY CHANGE THE IP ADDRESS

If for some reason you are having problems with the internet connection and cannot make the ddclient change the IP address for your freedns domain, try using the configuration below instead.

```sudo nano /etc/ddclient.conf```
```
 # Configuration file for ddclient generated by debconf
 #
 # /etc/ddclient.conf
 #
 # Check the current IP address. Either check the eth0 port for its current IP address (can't be used on a LAN),
 # or use the DynDNS IP checking service.
 daemon=3600
 pid=/var/run/ddclient.pid
 #use=if, if=eth0
 use=web, web=checkip.dyndns.com/, web-skip='IP Address'
 #
 # Login and change the values at the DynDNS site, using SSL.
 protocol=dyndns2
 ssl=yes
 server=members.dyndns.org
 login=myDynDNSusername
 password='myDynDNSuserpassword'
 mysite_1.dynds.org,mysite_2.dyndns.org,mysite_3.dyndns.org
 ```
 
 # Notes:
 
 - if this doesn't work, try changing web-skip to 'Current Address' 
 - Note that the password must be enclosed in quotation marks, e.g 'myDynDNSuserpassword'
 
 For more information, check the link below.
 
 https://help.ubuntu.com/community/DynamicDNS
 


    
