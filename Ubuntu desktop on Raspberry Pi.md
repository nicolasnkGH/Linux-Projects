# Ubuntu desktop on Raspberry Pi
I bought a Raspberry PI 4 with the intention of learning Linux and to practice on the terminal. Also, I found that the device
is capable of handling several several tasks and can be used for testing programming skills.

My first project with the Raspberry Pi was to replace the original OS (Raspbian) with Ubuntu Desktop 20.04.2.0 LTS. 

For this project, I utilized the script Desktopify to convert the Ubuntu server for Raspberry Pi to an Ubuntu Desktop version.

* Tools needed:

    - Etcher software to flash the OS image into the SD card
        - https://www.balena.io/etcher/

    - Ubuntu Server download
        - https://ubuntu.com/download/raspberry-pi

Proceed with the regular installation and run the commands:

Clone the project

    git clone https://github.com/wimpysworld/desktopify.git

Change your current directory to desktopify directory

    cd desktopify

Convert the server to a desktop

    sudo ./desktopify --de ubuntu

More information can be found on the repository desktopify.
