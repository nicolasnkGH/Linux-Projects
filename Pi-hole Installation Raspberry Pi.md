# Pi-hole
Pi-hole is a Network-wide ad blocking via your own Linux hardware.
The Pi-hole installation process can be found on their website and also in the repository pi-hole forked on my page.

Installation command:

```curl -sSL https://install.pi-hole.net | bash```

Another method is to manually download the installer and then run it.

```wget -O basic-install.sh https://install.pi-hole.net```

```sudo bash basic-install.sh```

After the installation process is over, make sure to set up all devices to use Pi-hole. There are two methods for that.

  - Method 1
    
    * Configure the router to use Pi-Hole's DNS server. Under DHCP/DNS configurations, choose to enable DHCP server and select the IP address of your device 
    that runs Pi-Hole.(Make sure that our server has a static IP address). After that, go to Pi-Hole's page and configure the IPv4 to be the same as your 
    server's IP (same IP as the device that runs PI-Hole) under the DNS tab. Uncheck all options for the Upstream DNS servers and add the custom 
    IPv4 address mentioned above.
    
  - Method 2
  
    * If not able to make this change or either the router does not support DHCP, make the changes manually in every device. This option is also valid for 
    those whom wants to only set up Pi-Hole in certain devices. Go to the device's network manager page and set up Pi's IP address as the DNS server.
    
    Complete information can be found on the forked repository called pi-hole on my page.
