ouijaBoard
==========
###Ouija board HARDWARE :

The Ouija Board is an opensource project that combine inexpensive hardware and free software. It is all linux based.

List of parts I used to build the piece (most of the parts can be replaced with similars... Its up to you):

1.Raspberry Pi model B
2.USB microphone (tested with the Kinobo USB 2.0 Microphone http://www.kinobo.co.uk/desktop-microphone.html)
3.USB WiFi dongle compatible with Raspberry Pi pleas check: http://elinux.org/RPi_USB_Wi-Fi_Adapters
4.(x2) stepper motors 28byj-48
5.
6.(x2) DR CNC Stepper Motor Flexible Coupling Coupler 5x6mm D20L25
7.M6-1 6MM x 1000mm 1meter Stainless Steel 304 SS Threaded Rod REPRAP 3D (this is a 1 meter rod from which I obtained 2 smaller rods that were attached to the stepper motors and function as linear actuators.
8.XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX

Continue.........................

###Ouija board SOFTWARE installation and configuration guide:

Created by: fito_segrera
http://fii.to/

Special thanks to the JasperProject http://jasperproject.github.io/

The ouijaBoard project operates using a Raspberry Pi. All the process lsted next is created for this device. All the process has been installed and tested on Raspbian...

###Method 1 (Eassy)

Download the Raspberry Pi Image from this link: http://fii.to/downloads/ouijaBoard.tar.gz unzip and create a new raspberry pi SD card with it. Please use an 8 GB Sd card for this (note: please make sure that the SD card you are ussing is supported by the RBpi... please see: http://elinux.org/RPi_SD_cards)

###Method 2 (The HARDCORE way)

2.1 Download Raspbian Install and Configure

To download and install Raspbian please follow the official guide here: http://www.raspberrypi.org/downloads/

After that continue with the configuration in this guide.

Configure Raspbian:

We’re now going to do some basic housekeeping and install some of the required libraries. You should SSH into your Pi with a command similar to the following. The IP address usually falls in the 192.168.2.3-192.168.2.10 range.

    ssh pi@192.168.2.3 # password (default): raspberry
    
Note: there are several ways of figuring out what the ip address of the RPi is. My recomendation, go for the easy, plug a monitor and a keyboard and login into the pi. 
username: pi 
paswword: raspberry
Make sure your pi is pluged to a network using an ethernet cable or wiFi dongle...
Then type "ifconfig" (without quotes...) you should see something like: 

    wlan0   Link encap:Ethernet  HWaddr 00:0f:13:29:18:e0  
            inet addr:192.168.43.153  Bcast:192.168.43.255  Mask:255.255.255.0
            UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
            RX packets:1200 errors:0 dropped:0 overruns:0 frame:0
            TX packets:901 errors:0 dropped:0 overruns:0 carrier:0
            collisions:0 txqueuelen:1000 
            RX bytes:111701 (109.0 KiB)  TX bytes:147082 (143.6 KiB)

Note that the ip address of the pi appears after "inet addr:" and is 192.168.2.3. At this point you could either SSH into your Rpi from your computer or continue with the pluged monitor, keyboard and mouse.

After you are in and confortable...
    
Run the following, select to ‘Expand Filesystem’ and restart your Pi:

    sudo raspi-config

Run the following commands to update Pi and some install some useful tools.

    sudo apt-get update
    sudo apt-get upgrade --yes
    sudo apt-get install vim git-core espeak python-dev python-pip bison libasound2-dev libportaudio-dev python-pyaudio     --yes

Plug in your USB microphone. Let’s open up an ALSA configuration file with the terminal text editor (nano):

    sudo nano /etc/modprobe.d/alsa-base.conf
    
Change the following line:

    options snd-usb-audio index=-2

To this:

    options snd-usb-audio index=0

Back in the shell, run:

    sudo alsa force-reload
    
To change the audio output of the RBpi type: (If instead of 1 you use 2 the output will be set for the HDMI)

    sudo amixer cset numid=3 1

Next, test that recording works (you may need to restart your Pi) by recording some audio with the following command:

    arecord temp.wav

Make sure you have speakers or headphones connected to the audio jack of your Pi. You can play back the recorded file:

    aplay -D hw:1,0 temp.wav


2.2 Install Pocketsphinx
Pocketsphinx is a opensource project for speech recognition. For mor information please see: http://cmusphinx.sourceforge.net/wiki/download/
  
Installation Instructions:
      
Let’s download and unzip the sphinxbase and pocketsphinx packages:
      
    wget http://downloads.sourceforge.net/project/cmusphinx/sphinxbase/0.8/sphinxbase-0.8.tar.gz
    wget http://downloads.sourceforge.net/project/cmusphinx/pocketsphinx/0.8/pocketsphinx-0.8.tar.gz
    tar -zxvf sphinxbase-0.8.tar.gz
    tar -zxvf pocketsphinx-0.8.tar.gz
      
Now we build and install sphinxbase:

    cd ~/sphinxbase-0.8/
    ./configure --enable-fixed
    make
    sudo make install
      
And pocketsphinx:

    cd ~/pocketsphinx-0.8/
    ./configure
    make
    sudo make install
      
Once the installations are complete, restart your Pi.


